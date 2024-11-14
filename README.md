
# Aplikasi penghitung kata

Aplikasi PenghitungKataFrame adalah alat penghitung kata berbasis Java dengan antarmuka grafis menggunakan Java Swing. Fitur utamanya meliputi:

Pencarian Kata: Input untuk mencari dan menghitung kemunculan kata tertentu dalam teks.
Penghitungan Kata Total: Menghitung jumlah total kata dalam teks.
Simpan Hasil: Mendukung penyimpanan hasil ke dalam berkas.
Aplikasi ini juga menampilkan hasil secara real-time saat pengguna mengetik, cocok untuk analisis cepat kata dalam teks.









## Authors

- Muhammad Rizki Insnai 2210010075


## Documentation

```
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.event.DocumentListener;
import javax.swing.event.DocumentEvent;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
/**
 *
 * @author asus0
 */
public class PenghitungKataFrame extends javax.swing.JFrame {

    
    
   
    

    public PenghitungKataFrame() {
       initComponents(); // Memanggil metode yang dihasilkan oleh GUI Builder

        // Menambahkan ActionListener untuk tombol "Cari"
        searchButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String kataCari = searchField.getText();  // Mengambil kata dari JTextField
                hitungPencarianKata(kataCari);  // Memanggil fungsi pencarian kata
            }
        });

        // Menambahkan ActionListener untuk tombol "Hitung"
        hitungButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String teks = textArea.getText();
                hitungKata(teks);  // Memanggil metode hitungKata saat tombol ditekan
            }
        });

        // Menambahkan DocumentListener untuk perhitungan real-time
        textArea.getDocument().addDocumentListener(new DocumentListener() {
            public void insertUpdate(DocumentEvent e) {
                hitungKata(textArea.getText());
            }

            public void removeUpdate(DocumentEvent e) {
                hitungKata(textArea.getText());
            }

            public void changedUpdate(DocumentEvent e) {
                hitungKata(textArea.getText());
            }
        });
        
         // Menambahkan ActionListener untuk tombol "Simpan"
            simpanButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                simpanKeFile();  // Memanggil fungsi untuk menyimpan teks dan hasil perhitungan
            }
        });
    }

    private void hitungKata(String teks) {
        // Menghitung jumlah kata
        String[] kataArray = teks.split("\\s+");
        int jumlahKata = kataArray.length;

        // Menghitung jumlah karakter (tanpa spasi)
        int jumlahKarakter = teks.replaceAll("\\s", "").length();

        // Menghitung jumlah kalimat
        int jumlahKalimat = teks.split("[.!?]+").length;  // Perbaikan pada bagian ini

        // Update label dengan hasil
        kataLabel.setText("Jumlah Kata: " + jumlahKata);
        karakterLabel.setText("Jumlah Karakter: " + jumlahKarakter);
        kalimatLabel.setText("Jumlah Kalimat: " + jumlahKalimat);
    }
    
    

    private void hitungPencarianKata(String kata) {
        String teks = textArea.getText();
        int count = teks.split("\\b" + kata + "\\b").length - 1;
        JOptionPane.showMessageDialog(this, "Kata ditemukan sebanyak: " + count + " kali.");
    }
    
     private void simpanKeFile() {
        // Membuat dialog untuk memilih file
        JFileChooser fileChooser = new JFileChooser();
        fileChooser.setDialogTitle("Simpan Teks dan Hasil Perhitungan");
        
        // Membuka dialog penyimpanan
        int userSelection = fileChooser.showSaveDialog(this);

        if (userSelection == JFileChooser.APPROVE_OPTION) {
            File fileToSave = fileChooser.getSelectedFile();

            try (FileWriter fileWriter = new FileWriter(fileToSave)) {
                // Menulis teks dan hasil perhitungan ke file
                String teks = textArea.getText();
                String hasilPerhitungan = "Jumlah Kata: " + kataLabel.getText() + "\n"
                                         + "Jumlah Karakter: " + karakterLabel.getText() + "\n"
                                         + "Jumlah Kalimat: " + kalimatLabel.getText();

                // Menyimpan ke file
                fileWriter.write("Teks:\n" + teks + "\n\n" + "Hasil Perhitungan:\n" + hasilPerhitungan);
                JOptionPane.showMessageDialog(this, "File berhasil disimpan!");
            } catch (IOException ex) {
                JOptionPane.showMessageDialog(this, "Terjadi kesalahan saat menyimpan file.");
            }
        }
    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jPanel2 = new javax.swing.JPanel();
        jScrollPane4 = new javax.swing.JScrollPane();
        jScrollPane3 = new javax.swing.JScrollPane();
        textArea = new javax.swing.JTextArea();
        kataLabel = new javax.swing.JLabel();
        hitungButton = new javax.swing.JButton();
        karakterLabel = new javax.swing.JLabel();
        kalimatLabel = new javax.swing.JLabel();
        searchField = new javax.swing.JTextField();
        searchButton = new javax.swing.JButton();
        simpanButton = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        textArea.setColumns(20);
        textArea.setRows(5);
        jScrollPane3.setViewportView(textArea);

        jScrollPane4.setViewportView(jScrollPane3);

        kataLabel.setText("Jumlah Kata");

        hitungButton.setText("Hitung");
        hitungButton.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                hitungButtonActionPerformed(evt);
            }
        });

        karakterLabel.setText("Jumlah karakter");

        kalimatLabel.setText("Jumlah Kalimat");

        searchButton.setText("Cari");
        searchButton.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                searchButtonActionPerformed(evt);
            }
        });

        simpanButton.setText("Simpan");

        javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
        jPanel2.setLayout(jPanel2Layout);
        jPanel2Layout.setHorizontalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addGap(25, 25, 25)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(kalimatLabel)
                    .addComponent(karakterLabel)
                    .addComponent(kataLabel)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(hitungButton)
                        .addGap(16, 16, 16)
                        .addComponent(searchButton)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(simpanButton))
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(jScrollPane4, javax.swing.GroupLayout.PREFERRED_SIZE, 249, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(18, 18, 18)
                        .addComponent(searchField, javax.swing.GroupLayout.PREFERRED_SIZE, 157, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addContainerGap(687, Short.MAX_VALUE))
        );
        jPanel2Layout.setVerticalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                    .addComponent(jScrollPane4, javax.swing.GroupLayout.PREFERRED_SIZE, 290, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(searchField, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addComponent(kataLabel)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addComponent(karakterLabel)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addComponent(kalimatLabel)
                .addGap(18, 18, 18)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(hitungButton)
                    .addComponent(searchButton)
                    .addComponent(simpanButton))
                .addContainerGap(536, Short.MAX_VALUE))
        );

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(0, 278, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(26, 26, 26)
                .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void hitungButtonActionPerformed(java.awt.event.ActionEvent evt) {                                             
        hitungButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String teks = textArea.getText();
                hitungKata(teks);
            }
        });


    }                                            

    private void searchButtonActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // TODO add your handling code here:
    }                                            

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        // Membuat dan menampilkan frame
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new PenghitungKataFrame().setVisible(true);
            }
        });
    
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton hitungButton;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JScrollPane jScrollPane3;
    private javax.swing.JScrollPane jScrollPane4;
    private javax.swing.JLabel kalimatLabel;
    private javax.swing.JLabel karakterLabel;
    private javax.swing.JLabel kataLabel;
    private javax.swing.JButton searchButton;
    private javax.swing.JTextField searchField;
    private javax.swing.JButton simpanButton;
    private javax.swing.JTextArea textArea;
    // End of variables declaration                   
}
```

