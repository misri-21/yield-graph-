using System;
using System.Drawing;
using System.Windows.Forms;

public class BarGraphForm : Form
{
    private int[] values = { 10, 25, 15, 40, 30 };

    public BarGraphForm()
    {
        this.Text = "Bar Graph Example";
        this.Size = new Size(600, 400);
        this.Paint += new PaintEventHandler(DrawBarGraph);
    }

    private void DrawBarGraph(object sender, PaintEventArgs e)
    {
        Graphics g = e.Graphics;
        Brush barBrush = Brushes.Blue;

        int barWidth = 50;
        int spacing = 20;
        int x = 50;
        int maxHeight = 200;

        int maxValue = 0;
        foreach (int val in values)
        {
            if (val > maxValue) maxValue = val;
        }

        for (int i = 0; i < values.Length; i++)
        {
            int barHeight = (int)((values[i] / (float)maxValue) * maxHeight);
            int y = 300 - barHeight;

            g.FillRectangle(barBrush, x, y, barWidth, barHeight);
            g.DrawString(values[i].ToString(), this.Font, Brushes.Black, x, y - 20);

            x += barWidth + spacing;
        }
    }

    [STAThread]
    public static void Main()
    {
        Application.EnableVisualStyles();
        Application.Run(new BarGraphForm());
    }
} 
