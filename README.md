# 🔧 Setup

[![Latest Stable Version](http://poser.pugx.org/caiquebispo/ai-agents-php/v)](https://packagist.org/packages/caiquebispo/ai-agents-php) [![Total Downloads](http://poser.pugx.org/caiquebispo/ai-agents-php/downloads)](https://packagist.org/packages/caiquebispo/ai-agents-php) [![Latest Unstable Version](http://poser.pugx.org/caiquebispo/ai-agents-php/v/unstable)](https://packagist.org/packages/caiquebispo/ai-agents-php) [![License](http://poser.pugx.org/caiquebispo/ai-agents-php/license)](https://packagist.org/packages/caiquebispo/ai-agents-php) [![PHP Version Require](http://poser.pugx.org/caiquebispo/ai-agents-php/require/php)](https://packagist.org/packages/caiquebispo/ai-agents-php)

### Installation

Install the package via Composer:

```bash
composer require caiquebispo/ai-agents-php
```

### Prerequisites

Make sure you have the `phpdotenv` package installed. You can install it via Composer:

In your laravel application you do not need to install the `vlucas/phpdotenv` package.

```bash
composer require vlucas/phpdotenv
```

### Configuring the `.env` file

In the root of your project, create a file named `.env` with the following variables:

```dotenv
OPENAI_API_KEY=""
OPENAI_MODEL=""
```

### In Code

```php

//Load the .env file
$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
$dotenv->load();
 
// Create a new chat model
$chat = new \CaiqueBispo\AiAgentsPHP\ChatModels\ChatGPT();

// Create a new agent
$agent = new \CaiqueBispo\AiAgentsPHP\Agents\TestingAgent($chat);
$agent->ask("Hello, is this working?"); // Yes, I am here. How can I help you today?
```

## 🤖 Creating a new agent
To create a new agent, you must extend the `BaseAgent` class and define any additional functionality.

**NOTE: If you want your agent to always call a function, you can extend the `FunctionsAgent` instead!**

The `prePrompt` property is the pre-prompt that is passed to the chat model. This should describe how you want the agent to think and act.

You can use traits in `AgentTraits` to add specific functionalities that you may need.

This is an example of an agent that can send text messages, perform calculations.

**This is the total code needed to create an agent.**
```php
class TestingAgent extends BaseAgent {

    use \CaiqueBispo\AiAgentsPHP\AgentTraits\MathTrait; // Access to math functions

    public string $prePrompt = "You are a helpful assistant";   // Pre-prompt
}
```

### Defining an agent function
To define an agent function, you must follow the PHP DocBlock to describe the parameters, return type, and method.

For the agent to have access to the function, you must include an additional parameter in the PHPDoc block called `@aiagent-description`. This should be a string that describes the function. Any functions that include this property in the agent class will be automatically made available to the agent.

Example of the `add` function:
```php
    /**
     * @param int $a
     * @param int $b
     * @return int
     * @aiagent-description Adds two numbers
     */
    public function add(int $a, int $b): int {
        return $a + $b;
    }
```

## 🧰 Agent Traits
Agent Traits can be used to add functionalities to an agent. Some are included in this package under the `AgentTraits` namespace.

`DateTrait` - Provides access to date functions (e.g., `compareDates` or `getCurrentDate`)

It is highly recommended that you place reusable functions in a trait and then add that trait to your agent.

## 📝 Chat Models

### Currently Supported
- GPT-3.5-turbo
- GPT-4

### Adding a new chat model
New models can be added by extending the `AbstractChatModel` class. This class provides the basic functionality needed to interact with the chat model.

## ❤️ Contributing
Opening new issues is encouraged if you have any questions, problems, or ideas.

Pull requests are also welcome!

[See our contribution guide](CONTRIBUTING.md)
