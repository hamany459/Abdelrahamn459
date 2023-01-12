# Abdelrahamn459
C#
using System;
using System.Windows.Forms;

namespace Midterm_Prev
{
    public partial class Form1 : Form
    {
        public Form1()
        { InitializeComponent(); }

        private void AddToBill_btn_Click(object sender, EventArgs e)
        {
            // using if else statmenet 

            if (CusName_TB.Text == "")
            {
                MessageBox.Show("Customer name is missing", "Customer Name Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                CusName_TB.Focus();
            }
            else if (comboBox1.SelectedItem == null || comboBox1.SelectedIndex == -1)
            {
                MessageBox.Show("Select Nuts", "Nuts Missing", MessageBoxButtons.OK, MessageBoxIcon.Error);
                comboBox1.Focus();
            }
            else if (retail_RadioBtn.Checked == false && wholeRadioBtn.Checked == false)
            {
                MessageBox.Show("Select the Sales Type", "Sales Type Missing", MessageBoxButtons.OK, MessageBoxIcon.Error);
                retail_RadioBtn.Focus();
            }
            else
            {
                // Essential Variables 
                double price = 0;
                int quantity = 0;
                double discount = 0;
                string salesType = "";

                // quantity textbox check 

                if (quantityTextBox.Text == "")
                {
                    MessageBox.Show("Please type the quantity", "No Quantity", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
                else
                {
                    // using try - catch to extract values 
                    try
                    {
                        quantity = int.Parse(quantityTextBox.Text);


                        // take sales type automatically 
                        if (retail_RadioBtn.Checked == true)
                            salesType = retail_RadioBtn.Text;
                        else
                            salesType = wholeRadioBtn.Text;
                        // Calculate the amount of nuts and discount using switch statements 
                        switch (comboBox1.SelectedIndex)
                        {
                            case 0:
                                price = 3.5; break;
                            case 1:
                                price = 4.5; break;
                            case 2:
                                price = 4.5; break;
                            case 3:
                                price = 4.0; break;
                            case 4:
                                price = 4.5; break;
                            case 5:
                                price = 1.5; break;
                        }// switch 
                        DetailsListbox.Items.Add
                            (salesType + "\t\t" + comboBox1.SelectedItem.ToString() + "\t\t" + price + "\t" + quantity);

                        // Calculate Amount 

                        double amount = quantity * price;
                        AmountListbox.Items.Add(amount);
                    }
                    catch (Exception s)
                    {
                        MessageBox.Show(s.Message, "Exceptional Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        quantityTextBox.Focus();
                    }
                }
            }// else 

        }

        private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
        {
            double price = 0;
            switch (comboBox1.SelectedIndex)
            {
                case 0:
                    price = 3.5; break;
                case 1:
                    price = 4.5; break;
                case 2:
                    price = 4.5; break;
                case 3:
                    price = 4.0; break;
                case 4:
                    price = 4.5; break;
                case 5:
                    price = 1.5; break;
            }// switch 

            priceTextBox.Text = price.ToString("C");
        }

        private void Clear_btn_Click(object sender, EventArgs e)
        {
            //deselecting and removing texts to enter new data with same customer 
            quantityTextBox.Clear();
            comboBox1.SelectedIndex = -1;
            retail_RadioBtn.Checked = false;
            wholeRadioBtn.Checked = false;
        }

        private void Bill_btn_Click(object sender, EventArgs e)
        {
            Random rand = new Random();
            int Random_invoice_number = rand.Next(100, 100000);
            string date = DateTime.Now.ToShortDateString();
            string customerName = CusName_TB.Text;
            double total = 0;

            foreach (var s in AmountListbox.Items)
            {
                total += Convert.ToDouble(s.ToString());
            }

            MessageBox.Show("Invoice No: " + Random_invoice_number +
                "\nDate: " + date +
                "\nCustomer Name: " + customerName +
                "\nTotal Bill Amount = " + total.ToString("C") + ""
                , "Bill", MessageBoxButtons.OK, MessageBoxIcon.Information);

            // THIS IS JUST FOR FUN NOT STATED IN THE QUESTION 
            dateTB.Text = date;
            invoiceNum_TB.Text = Random_invoice_number.ToString();

        }

        private void restBtn_Click(object sender, EventArgs e)
        {
            quantityTextBox.Clear();
            CusName_TB.Clear();
            DetailsListbox.Items.Clear();
            AmountListbox.Items.Clear();
            priceTextBox.Clear();

            comboBox1.SelectedIndex = -1;
            retail_RadioBtn.Checked = false;
            wholeRadioBtn.Checked = false;
        }

        private void AddNutsBtn_Click(object sender, EventArgs e)
        {
            if (comboBox1.Text == "")
            {
                MessageBox.Show("Please type Nuts name", "No nuts name typed", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            else
            {
                bool item_exist = false;
                foreach (var s in comboBox1.Items)
                {
                    if (s.Equals(comboBox1.Text))
                    {
                        item_exist = true;
                        MessageBox.Show("Nuts Already exist", "Dupllicate Nuts", MessageBoxButtons.OK, MessageBoxIcon.Information);
                        break;
                    }
                }// foreach loop 
                if (item_exist == false)
                {
                    comboBox1.Items.Add(comboBox1.Text);
                }
            }
        }

        private void AboutBtn_Click(object sender, EventArgs e)
        {
            MessageBox.Show(
                "Student Name : ZORO MORO" +
                "Student ID : 414####",
                "Studnet Information",
                MessageBoxButtons.OK, MessageBoxIcon.Information
                );
        }
    }
}
