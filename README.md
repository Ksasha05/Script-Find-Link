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
            for (int i = 0; i < list.Count; i++)
            {
                web.Navigate().GoToUrl(list[i]);
                text = web.PageSource;
                //richTextBox1.AppendText(text);

                string filepath = Path.Combine(Environment.CurrentDirectory, "output.txt");

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











