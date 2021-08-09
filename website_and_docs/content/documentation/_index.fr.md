---
title: "Le Projet d'Automatisation de Navigateur Selenium"
linkTitle: "Documentation"
cascade:
- type: docs
aliases: ["/documentation/fr/"]
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to French. Do you speak French? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

Selenium est projet englobant un éventail d'outils et de librairies
permettant l'automtisation des navigateurs internet.

Il fournit des extensions afin d'émuler des interactions utilisateur avec les navigateurs, 
un serveur de distribution permettant la mise à l'échelle de l'allocation de navigateur 
ainsi que l'infrastructure pour l'implémentation de la [spécification W3C WebDriver](//www.w3.org/TR/webdriver/)
permettant l'écriture de code interchangeable pour tous les principaux navigateurs.

Ce projet est rendu possible grâce au contributeurs volontaires 
ayant investi des milliers d'heures de leur temps 
et rendu le code source [disponible librement]({{< ref "/copyright_and_attributions.md#license" >}})
à quiconque souhaitant l'utiliser et l'améliorer ou simplement s'amuser.

Selenium rassemble distributeurs de navigateur, ingénieurs et entousiastes
pour favoriser une discussion ouverte autour de l'automatisation de la platerforme web.
Le projet organise [une conférence annuelle](//seleniumconf.com/) afin d'entretenir cette communauté.

Au coeur de Selenium se trouve [WebDriver]({{< ref "/webdriver.md" >}}), 
une interface permettant d'écrire des instructions pouvant être exécutées indifférement par de nombreux navigateurs.
Voici par exemple une des plus simples instructions disponibles:


{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.WebDriverWait;
import static org.openqa.selenium.support.ui.ExpectedConditions.presenceOfElementLocated;
import java.time.Duration;

public class HelloSelenium {

    public static void main(String[] args) {
        WebDriver driver = new FirefoxDriver();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        try {
            driver.get("https://google.com/ncr");
            driver.findElement(By.name("q")).sendKeys("cheese" + Keys.ENTER);
            WebElement firstResult = wait.until(presenceOfElementLocated(By.cssSelector("h3")));
            System.out.println(firstResult.getAttribute("textContent"));
        } finally {
            driver.quit();
        }
    }
}
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support.expected_conditions import presence_of_element_located

#This example requires Selenium WebDriver 3.13 or newer
with webdriver.Firefox() as driver:
    wait = WebDriverWait(driver, 10)
    driver.get("https://google.com/ncr")
    driver.find_element(By.NAME, "q").send_keys("cheese" + Keys.RETURN)
    first_result = wait.until(presence_of_element_located((By.CSS_SELECTOR, "h3")))
    print(first_result.get_attribute("textContent"))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using System;
using OpenQA.Selenium;
using OpenQA.Selenium.Firefox;
using OpenQA.Selenium.Support.UI;

class HelloSelenium {
  static void Main() {
    using(IWebDriver driver = new FirefoxDriver()) {
      WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
      driver.Navigate().GoToUrl("https://www.google.com/ncr");
      driver.FindElement(By.Name("q")).SendKeys("cheese" + Keys.Enter);
      wait.Until(webDriver => webDriver.FindElement(By.CssSelector("h3")).Displayed);
      IWebElement firstResult = driver.FindElement(By.CssSelector("h3"));
      Console.WriteLine(firstResult.GetAttribute("textContent"));
    }
  }
}
  {{< /tab >}}
  {{< tab header="Ruby" >}}
require 'selenium-webdriver'

driver = Selenium::WebDriver.for :firefox
wait = Selenium::WebDriver::Wait.new(timeout: 10)

begin
  driver.get 'https://google.com/ncr'
  driver.find_element(name: 'q').send_keys 'cheese', :return
  first_result = wait.until { driver.find_element(css: 'h3') }
  puts first_result.attribute('textContent')
ensure
  driver.quit
end
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const {Builder, By, Key, until} = require('selenium-webdriver');

(async function example() {
    let driver = await new Builder().forBrowser('firefox').build();
    try {
        // Navigate to Url
        await driver.get('https://www.google.com');

        // Enter text "cheese" and perform keyboard action "Enter"
        await driver.findElement(By.name('q')).sendKeys('cheese', Key.ENTER);

        let firstResult = await driver.wait(until.elementLocated(By.css('h3')), 10000);

        console.log(await firstResult.getAttribute('textContent'));
    }
    finally{
        driver.quit();
    }
})();
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
import org.openqa.selenium.By
import org.openqa.selenium.Keys
import org.openqa.selenium.firefox.FirefoxDriver
import org.openqa.selenium.support.ui.ExpectedConditions.presenceOfElementLocated
import org.openqa.selenium.support.ui.WebDriverWait
import java.time.Duration

fun main() {
    val driver = FirefoxDriver()
    val wait = WebDriverWait(driver, Duration.ofSeconds(10))
    try {
        driver.get("https://google.com/ncr")
        driver.findElement(By.name("q")).sendKeys("cheese" + Keys.ENTER)
        val firstResult = wait.until(presenceOfElementLocated(By.cssSelector("h3")))
        println(firstResult.getAttribute("textContent"))
    } finally {
        driver.quit()
    }
}
  {{< /tab >}}
{{< /tabpane >}}



See the [Overview]({{< ref "/overview.md" >}}) to check the different project 
components and decide if Selenium is the right tool for you.

You should continue on to [Getting Started]({{< ref "/getting_started.md" >}})
to understand how you can install Selenium and successfully use it as a test 
automation tool, and scaling simple tests like this to run in large, distributed 
environments on multiple browsers, on several different operating systems.
