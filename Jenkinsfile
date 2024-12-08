const webdriver = require('selenium-webdriver');
const assert = require('assert');
const driver = new webdriver.Builder().forBrowser('chrome').build();

async function runTest() {
    try {
        // Open the HTML file in the browser
        await driver.get('file://' + __dirname + '/index.html');

        // Test Addition
        const num1 = await driver.findElement(webdriver.By.id('num1'));
        await num1.sendKeys('50');
        const num2 = await driver.findElement(webdriver.By.id('num2'));
        await num2.sendKeys('10');

        const addButton = await driver.findElement(webdriver.By.id('add'));
        await addButton.click();

        const addResult = await driver.findElement(webdriver.By.id('result'));
        const addText = await addResult.getText();
        assert.strictEqual(addText, '60', 'Addition calculation is incorrect');

        console.log('Test passed: Addition is correct');

        // Clear inputs for subtraction test
        await num1.clear();
        await num2.clear();

        // Test Subtraction
        await num1.sendKeys('50');
        await num2.sendKeys('10');

        const subtractButton = await driver.findElement(webdriver.By.id('subtract'));
        await subtractButton.click();

        const subtractResult = await driver.findElement(webdriver.By.id('result'));
        const subtractText = await subtractResult.getText();
        assert.strictEqual(subtractText, '40', 'Subtraction calculation is incorrect');

        console.log('Test passed: Subtraction is correct');
    } catch (error) {
        console.error('Test failed:', error);
    } finally {
        // Wait for user input to close the browser
        console.log('Press any key to exit...');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', async () => {
            await driver.quit();
            process.exit(0);
        });
    }
}

runTest();
