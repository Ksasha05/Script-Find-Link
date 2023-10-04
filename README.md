# Script-Find-Link
Скрипт для поиска ссылки на странице<br>

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using OpenQA;
using OpenQA.Selenium;
using OpenQA.Selenium.Edge;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Style;


namespace nalichie
{
    public partial class Form1 : Form
    {
        IWebDriver web = new EdgeDriver();
        public string path, text, word1, word2;
        public List<string> list = new List<string>();
        

        public Form1()
        {
            InitializeComponent();
        }

        private void button3_Click(object sender, EventArgs e)
        {
            string filepath = Path.Combine(Environment.CurrentDirectory, "input.txt");
            using (StreamReader sr = new StreamReader(filepath))
            {
                while (!sr.EndOfStream)
                {
                    list.Add(sr.ReadLine());
                }

                for (int i = 0; i < list.Count; i++)
                {
                    //MessageBox.Show(list[i]);
                    richTextBox3.AppendText(list[i] + "\n");
                }
            }
        }

        private void button1_Click(object sender, EventArgs e)
        {
            var Articles = new[]
            {
                new {
                    Id = "101", Name = "C++"
                },
                new {
                    Id = "102", Name = "Python"
                },
                new {
                    Id = "103", Name = "Java Script"
                },
                new {
                    Id = "104", Name = "GO"
                },
                new {
                    Id = "105", Name = "Java"
                },
                new {
                    Id = "106", Name = "C#"
                }
            };

            //string filepath_xlsx = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

            for (int i = 0; i < list.Count; i++)
            {
                web.Navigate().GoToUrl(list[i]);
                text = web.PageSource;
                //richTextBox1.AppendText(text);

                string filepath = Path.Combine(Environment.CurrentDirectory, "output.txt");

                /*ExcelPackage excel = new ExcelPackage();
                var workSheet = excel.Workbook.Worksheets.Add("Sheet1");
                workSheet.DefaultRowHeight = 12;

                workSheet.Row(1).Height = 20;
                workSheet.Row(1).Style.HorizontalAlignment = ExcelHorizontalAlignment.Center;
                workSheet.Row(1).Style.Font.Bold = true;

                workSheet.Cells[1, 1].Value = "S.No";
                workSheet.Cells[1, 2].Value = "Id";
                workSheet.Cells[1, 2].Value = "Name";

                
                //FileInfo excelFile = new FileInfo(Path.Combine(Environment.CurrentDirectory, "exel.xlsx"));
                string excelFilePath = Path.Combine(Environment.CurrentDirectory, "exel.xlsx");
                if (File.Exists(excelFilePath))
                    File.Delete(excelFilePath);

                FileStream fs = File.Create(excelFilePath);
                File.WriteAllBytes(excelFilePath, excel.GetAsByteArray());

                excel.Dispose();*/

                /*int recordIndex = 2;
                foreach(var article in Articles)
                {
                    workSheet.Cells[recordIndex, 1].Value = (recordIndex - 1).ToString();
                }*/



                using (StreamWriter sw = File.Exists(filepath) ? File.AppendText(filepath) : File.CreateText(filepath))
                {
                    word1 = "https://ggsel.net";
                    word2 = "https://ggsel.com";
                    int position = text.IndexOf(word1);
                    int positionn = text.IndexOf(word2);
                    if (position >= 0 || positionn >= 0)
                    {
                        richTextBox2.AppendText($"{list[i]} - Ссылка есть\n");
                        sw.WriteLine($"{path} - Ссылка есть");
                    }
                    else
                    {
                        richTextBox2.AppendText($"{list[i]} - Ссылки нет\n");
                        sw.WriteLine($"{path} - Ссылки нет");
                    }
                }
                //richTextBox1.Clear();
            }
        }
    }
}

```











