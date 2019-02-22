# Jsoup

En este proyecto se basaba de coger información de una pagina web en javafx. Yo he tenido problemas con Java FX y lo he hecho con java swing.

```java 
import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JLabel;
import java.awt.event.ActionListener;
import java.io.IOException;
import java.util.ArrayList;
import java.awt.event.ActionEvent;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.ItemListener;
import java.awt.event.ItemEvent;

public class Scrapi extends JFrame {

	private JPanel contentPane;
	

	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Scrapi frame = new Scrapi();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	public Scrapi() {
		ArrayList<String> lista = new ArrayList<String>();
		
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 450, 300);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);
		
		JButton btnActualizar = new JButton("Actualizar");
		
		btnActualizar.setBounds(169, 227, 89, 23);
		contentPane.add(btnActualizar);
		
		JComboBox comboBox = new JComboBox();
		
		
		
		comboBox.setBounds(88, 101, 213, 23);
		contentPane.add(comboBox);
		
		JLabel lblNewLabel = new JLabel("");
		lblNewLabel.setBounds(88, 156, 213, 14);
		contentPane.add(lblNewLabel);
		
		JLabel label = new JLabel("");
		label.setBounds(88, 28, 203, 14);
		contentPane.add(label);
		
		btnActualizar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				try {
					comboBox.removeAll();
		            Document doc= Jsoup.connect("https://www.levante-emv.com/").get();

		            String title=doc.title();
		            label.setText(title);

		            Elements links=doc.select("a[href]");
		            for (Element link: links) {
		            	lista.add(link.attr("href"));
		            	lista.add(link.text());
		                
		            	comboBox.addItem(link.attr("href"));
		            }
		        } catch (IOException e) {
		            e.printStackTrace();
		        }
			}
		});
		
		comboBox.addMouseListener(new MouseAdapter() {
			@Override
			public void mousePressed(MouseEvent e) {
				int i=(int) comboBox.getSelectedItem();
				lblNewLabel.setText(lista.get(i));
					
			}
		});
	}
}


```
