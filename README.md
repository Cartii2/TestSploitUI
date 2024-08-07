using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using ccapi;
using FastColoredTextBoxNS;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        public Point mouseLocation;
        public Form1()
        {
            InitializeComponent();
        }

        private void panel1_Paint(object sender, PaintEventArgs e)
        {
            
        }

        private void mouse_Down(object sender, MouseEventArgs e)
        {

            mouseLocation = new Point(-e.X, -e.Y);
        }

        private void mouse_Move(object sender, MouseEventArgs e)
        {
            if (e.Button == MouseButtons.Left)
            {
                Point mousePose = Control.MousePosition;
                mousePose.Offset(mouseLocation.X, mouseLocation.Y);
                Location = mousePose;
            }
        }

        private void button1_Click(object sender, EventArgs e)
        {
            ccapi.ExploitApi.Execute(fastColoredTextBox1.Text);

        }

        private void label2_Click(object sender, EventArgs e)
        {
            this.WindowState = System.Windows.Forms.FormWindowState.Minimized;
        }

        private void button2_Click(object sender, EventArgs e)
        {
            fastColoredTextBox1.Text = string.Empty;
        }

        private void button3_Click(object sender, EventArgs e)
        {
            openFileDialog1.ShowDialog();
            string filename = openFileDialog1.FileName;
            string readfile = File.ReadAllText(filename);
            fastColoredTextBox1.Text = readfile;
        }

        private void button4_Click(object sender, EventArgs e)
        {
            SaveFileDialog saveFileDialog1 = new SaveFileDialog();
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                using (Stream s = File.Open(saveFileDialog1.FileName, FileMode.CreateNew))
                using (StreamWriter sw = new StreamWriter(s))
                {
                    sw.Write(fastColoredTextBox1.Text);
                }
            }
        }

        private void fastColoredTextBox1_Load(object sender, EventArgs e)
        {
            fastColoredTextBox1.Language = FastColoredTextBoxNS.Language.Lua;
        }

        private void button6_Click(object sender, EventArgs e)
        {
          
        }

        private void button5_Click(object sender, EventArgs e)
        {

            string injectpath = Path.Combine(Application.StartupPath, "api", "CeleryInject.exe");
            ccapi.ExploitApi.Inject(injectpath, true, false);

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void label1_Click(object sender, EventArgs e)
        {
            Close();
        }
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------
Form 2 code
--------------
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form2 : Form
    {
        public Form2()
        {
            InitializeComponent();
        }

        private void button4_Click(object sender, EventArgs e)
        {
            while (true) { Process[] proc = Process.GetProcessesByName("RobloxPlayerBeta"); foreach (Process p in proc) { p.Kill(); } }
        }

        private void Form2_Load(object sender, EventArgs e)
        {

        }
    }
}
