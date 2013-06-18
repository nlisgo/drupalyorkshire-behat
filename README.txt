curl -sS https://getcomposer.org/installer | php
php composer.phar install

./bin/behat --init

# features/bootstrap/FeatureContext.php
use Behat\MinkExtension\Context\MinkContext;
class FeatureContext extends MinkContext

./bin/behat -dl

# behat.yml
default:
  extensions:
    Behat\MinkExtension\Extension:
      base_url: http://en.wikipedia.org
      goutte: ~
      selenium2: ~

# features/search.feature
Feature: Search
  In order to see a word definition
  As a website user
  I need to be able to search for a word

  Scenario: Searching for a page that does exist
    Given I am on "/wiki/Main_Page"
    When I fill in "search" with "Behavior Driven Development"
    And I press "searchButton"
    Then I should see "agile software development"

  Scenario: Searching for a page that does NOT exist
    Given I am on "/wiki/Main_Page"
    When I fill in "search" with "Glory Driven Development"
    And I press "searchButton"
    Then I should see "Search results"

  @javascript
  Scenario: Searching for a page with autocompletion
    Given I am on "/wiki/Main_Page"
    When I fill in "search" with "Behavior Driv"
    And I wait for the suggestion box to appear
    Then I should see "Behavior-driven development"

# features/bootstrap/FeatureContext.php
    /**
     * @Given /^I wait for the suggestion box to appear$/
     */
    public function iWaitForTheSuggestionBoxToAppear()
    {
        $this->getSession()->wait(5000,
            "$('.suggestions-results').children().length > 0"
        );
    }

