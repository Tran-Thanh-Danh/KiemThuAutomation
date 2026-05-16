using System;
using System.Collections.Generic;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using OpenQA.Selenium.Support.UI;
using NUnit.Framework;

namespace BlazeDemo.Tests
{
    [TestFixture]
    public class BlazeDemoTest
    {
        private IWebDriver driver;

        [SetUp]
        public void SetUp()
        {
            var options = new ChromeOptions();
            options.AddArgument("--headless");
            options.AddArgument("--no-sandbox");
            options.AddArgument("--disable-gpu");
            options.AddArgument("--disable-dev-shm-usage");

            driver = new ChromeDriver(options);
            driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(10);
        }

        [TearDown]
        protected void TearDown()
        {
            driver.Quit();
            driver.Dispose();
        }

        // --- TEST CASE 1: Mua vé E2E (Luồng cũ của bạn) ---
        [Test]
        public void TC01_PurchaseFlight_Successful()
        {
            driver.Navigate().GoToUrl("https://blazedemo.com/");
            
            new SelectElement(driver.FindElement(By.Name("fromPort"))).SelectByValue("Paris");
            new SelectElement(driver.FindElement(By.Name("toPort"))).SelectByValue("London");
            driver.FindElement(By.CssSelector(".btn-primary")).Click();
            
            driver.FindElement(By.CssSelector("tr:nth-child(1) .btn")).Click();
            
            driver.FindElement(By.Id("inputName")).SendKeys("Nguyen Van A");
            driver.FindElement(By.CssSelector(".btn-primary")).Click();
            
            Assert.That(driver.FindElement(By.CssSelector("h1")).Text, Is.EqualTo("Thank you for your purchase today!"));
        }

        // --- TEST CASE 2: Kiểm tra Điều hướng Link (Navigation) ---
        [Test]
        public void TC02_Verify_DestinationOfTheWeek_Link()
        {
            driver.Navigate().GoToUrl("https://blazedemo.com/");
            
            // Tìm và click vào link "destination of the week! The Beach!"
            driver.FindElement(By.LinkText("destination of the week! The Beach!")).Click();
            
            // Xác nhận URL mới có chứa chữ "vacation.html"
            Assert.That(driver.Url, Does.Contain("vacation.html"));
        }

        // --- TEST CASE 3: Kiểm tra Dữ liệu Động (Dynamic Data) ---
        [Test]
        public void TC03_Verify_Dynamic_Flight_Header()
        {
            driver.Navigate().GoToUrl("https://blazedemo.com/");
            
            // Chọn chuyến bay từ Boston đi Rome
            new SelectElement(driver.FindElement(By.Name("fromPort"))).SelectByValue("Boston");
            new SelectElement(driver.FindElement(By.Name("toPort"))).SelectByValue("Rome");
            driver.FindElement(By.CssSelector(".btn-primary")).Click();
            
            // Kiểm tra thẻ h3 có in đúng thông tin 2 thành phố vừa chọn không
            var headerText = driver.FindElement(By.TagName("h3")).Text;
            Assert.That(headerText, Is.EqualTo("Flights from Boston to Rome:"));
        }

        // --- TEST CASE 4: Kiểm tra Bảng dữ liệu (Table Elements) ---
        [Test]
        public void TC04_Verify_Flights_Table_Has_Data()
        {
            driver.Navigate().GoToUrl("https://blazedemo.com/");
            driver.FindElement(By.CssSelector(".btn-primary")).Click(); // Đi thẳng tới bảng chuyến bay
            
            // Đếm số lượng hàng (chuyến bay) có trong bảng
            var rows = driver.FindElements(By.CssSelector("table tbody tr"));
            
            // Khẳng định bảng phải có dữ liệu (lớn hơn 0 hàng)
            Assert.That(rows.Count, Is.GreaterThan(0));
        }

        // --- TEST CASE 5: Kiểm tra Label Giao diện (UI Element Presence) ---
        [Test]
        public void TC05_Verify_TotalCost_Is_Displayed()
        {
            driver.Navigate().GoToUrl("https://blazedemo.com/purchase.php");
            
            // Lấy toàn bộ chữ trong form thông tin
            var bodyText = driver.FindElement(By.TagName("body")).Text;
            
            // Khẳng định trang web có hiển thị trường "Total Cost" cho người dùng
            Assert.That(bodyText, Does.Contain("Total Cost"));
        }
    }
}