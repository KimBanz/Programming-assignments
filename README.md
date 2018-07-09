using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        //User puts something into text boxes
        //First step is to save data
        //then they click Save
        //that triggers btnSave_Click
        //Create SaveFileDialog, and display with ShowDialog()
        //User can specify where
        //collect the sata and turn it into a string with CSV
        //Write it, then tell them it's done

        

        private void btnSave_Click_1(object sender, EventArgs e)
        {
            SaveFileDialog dialog = new SaveFileDialog();
            DialogResult result = dialog.ShowDialog();

            //create the IF condition because User may or may not have specified

            if (result == DialogResult.OK)
            {
                string alldata1 = "{0},{1},{2},{3},{4}";
                //because computers start at 0
                //this is making an array
                //tells the computer the thing called "alldata" gets converted
                //with the stuff that follows and replaces the numbers with the strings
                string final = string.Format(alldata1, txtFirstName.Text, txtLastName.Text, txtLikes.Text, txtDislikes.Text, txtBirthday.Text);

                //now write the CSV into the file specified by user
                string userSpecifiedFile = dialog.FileName;
                System.IO.File.WriteAllText(userSpecifiedFile, final);
                //Tell user this was a success
                MessageBox.Show("Got it!");
            }
        }

        private void btnLoad_Click_1(object sender, EventArgs e)
        {
            //Use the OpenFile Dialog to give user the chance to load data
            OpenFileDialog dialog = new OpenFileDialog();
            DialogResult result = dialog.ShowDialog();

            //add the IF loop when condition is true
            if (result == DialogResult.OK)
            {
                //Assuming it's true, read the text from the files
                string userSpecifiedFile = dialog.FileName;
                string fileData = System.IO.File.ReadAllText(userSpecifiedFile);

                //Now split it, using the comma in an array
                string[] elements = fileData.Split(',');

                //Copy those elements onto the screen
                //The data was saved as First,Last,Likes,Dislikes,Birthday
                //so the array starts at 0 and gets split and returned in that same way
                txtFirstName.Text = elements[0];
                txtLastName.Text = elements[1];
                txtLikes.Text = elements[2];
                txtDislikes.Text = elements[3];
                txtBirthday.Text = elements[4];
            }
        }
    }
}
    

    

