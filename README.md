# Product-Storage-System
/* about project
"Product Storage System" , merupakam sebuah program yang di desain untuk media info penyimpanan list item berupa makanan (Food/Beverage). 
Dengan program ini kita bisa mencatat nama item, tipe (Food/Beverage), dan jumlah item secara digital. 
Jika terjadi kesalahan pada pencatatan, maka data tersebut dapat diubah dan diupdate. 
Fitur Program :
1. Insert Product, yang terdiri atas product type, product name dan product quantity 
2. Show All Product - Sorting by Smallest Quantity, merupakan pilihan untuk menampilkan semua jenis makanan atau minuman yang sudah di input dan mengelompokkannya dari produk dengan kuantitas terendah hingga terbanyak
3. Edit Product, merupakan fitur untuk mengedit / update nama produk, tipe ataupun kuantitas nya.
4. Delete All, merupakan fitur untuk menghapus item secara keseluruhan (nama, tipe dan kuantitas )
5. Produk Details, merupakan fitur untuk melihat info per produk */

//Code

import java.text.NumberFormat;
import java.util.Scanner;
import java.util.Vector;

public class Main {
	Scanner scan = new Scanner(System.in);
	public Vector <String> productNameList = new Vector<>();
	public Vector <String> productTypeList = new Vector<>();
	public Vector <Integer> productQtyList = new Vector<>();

	public Main() {
  
		int choose = 0;
		do {
			System.out.println("==========================");
			System.out.println("+ Product Storage System +");
			System.out.println("==========================");
			System.out.println("");
			System.out.println("1.Insert Product");
			System.out.println("2.Show all Product - Sort By Smallest Quantity");
			System.out.println("3.Edit Product");
			System.out.println("4.Delete  all Product");
			System.out.println("5.Product Details");
			System.out.println("6.Exit");
			System.out.print("Choose >>>");
			choose = scan.nextInt();
			scan.nextLine();
			
			if(choose == 1) {
				insertProduct();	
			}
			
			else if(choose == 2) {
				sortBySmallestQuantity();
				view();
			}
			
			else if(choose == 3) {
				updateProduct();
			}
			
			else if(choose == 4) {
				deleteProduct();
			}
			
			else if(choose == 5) {
				productDetails();
			}
			
			else if (choose == 6) {
				System.out.println("Thank you for using our program");
			}
			
		
			} while ( choose != 6);
		
	}

	public static void main(String[] args) {
		new Main();
	}
	
	
	public Integer seacrhProduct(String productName){
		Integer idx = -1;
		for(int i = 0; i < productNameList.size(); i++) {
			if(productNameList.get(i).equals(productName)) {
				idx = i;
			}
		}
		return idx;
	}
	
	public void insertProduct() {
		String name = "";
		String type = "";
		Integer Qty = 0;
		int checkIndex = -1;
		
		do {
			type = "";
			System.out.print("Insert product type here [Food|Beverage | Case Sensitive] :");
			type = scan.nextLine();
		}while(!type.equals("Food") && !type.equals("Beverage"));
		
		do {
			name ="";
			System.out.print("Insert product name here[Product min.6 characters, max.25 characters] :");
			name = scan.nextLine();	
			
			checkIndex = seacrhProduct(name);
			if(checkIndex > -1) {
				System.out.println("Product already in the list !");
			}
		}while((name.length()< 6 || name.length() > 25) && checkIndex != -1);
		
		do {
			Qty = 0;
			try {
				System.out.print("Input the quantity: ");
				Qty = scan.nextInt();
				
			} catch (Exception e) {
				System.out.println("The input must be numeric ! ");
				Qty = -1;
				scan.nextLine();
			}
		} while (Qty < 1 || Qty > 100);
	 
		productNameList.add(name);
		productTypeList.add(type);
		productQtyList.add(Qty);
	 
	}
