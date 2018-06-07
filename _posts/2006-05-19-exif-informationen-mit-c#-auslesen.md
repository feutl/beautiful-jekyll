---
layout: post
title: EXIF Informationen mit C# auslesen
date: 2006-05-19
tags: [deutsch, technology]
bigimg: /img/2006/exifextractor.png
---


In der Zeit der Multimediaanwendungen sollten man doch glauben, dass das Auslesen von EXIF Informationen aus JPG Bildern in einem aktuellen Framework wie .Net 2.0 ein Kinderspiel sein sollte. Doch entweder hab ich es mal wieder nicht gefunden wie es geht oder es hat sich einfach seit dem .Net 1.1 in dieser Hinsicht nichts geändert.

![ExifExtractor](/img/2006/exifextractor.png)

Egal - es waren dann im Endeffekt zwar wenige Codezeilen, doch die Zeit verging wie im Flug beim Durchforsten verschiedenster Sites.

* [EXIFextractor library to extract EXIF information](http://www.codeproject.com/csharp/exifextractor.asp)
* [Meta Data Extractor in C#](http://renaud91.free.fr/MetaDataExtractor/)
* [EXIF metadata from .JPG weirdness](http://www.dotnet247.com/247reference/msgs/35/178243.aspx)

Und hier mein Ergebnis in Code Form, denn die GUI gibt es eh als EntryIcon zum Vergrößern ein Stückerl weiter ob ;) Verwendet wurden:
* PictureBox
* DataGridView
* Label
* Button

```c#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Drawing.Imaging;
using System.Text;
using System.Windows.Forms;

namespace ExifExtraction
{
    public partial class Form1 : Form
    {
        public Form1() 
        {
            InitializeComponent();
        }
        private void btnLoad_Click(object sender, EventArgs e) 
        {
            DialogResult imageLocation = openFileDialog1.ShowDialog();
            dataGridView1.Rows.Clear();
            if (DialogResult.OK == imageLocation)
            {
                picLoaded.Image = Image.FromFile(openFileDialog1.FileName);
                Image imgLoaded = Image.FromFile(openFileDialog1.FileName);
                foreach (PropertyItem item in imgLoaded.PropertyItems)
                {
                     //alle Infos auslesen - item.Id beinhaltet die Position der spezifischen Information
                     dataGridView1.Rows.Add();
                     dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[0].Value = item.Id;
                     dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[1].Value = System.Text.Encoding.Default.GetString(item.Value);
                     // Datum und Uhrzeit auslesen
                     if (item.Id == 306) lblDateTime.Text = System.Text.Encoding.Default.GetString(item.Value);
                }
            }
        }
    }
}
```