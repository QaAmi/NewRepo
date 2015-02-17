# NewRepo 
# Question number - 4 - In-Memory File System


import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.io.Writer;
import java.util.*;

import org.omg.CORBA.portable.OutputStream;


public class InMemoryFileSys {

	
	public static void main(String[] args) throws IOException {
		
		
	String folder =  "C:/Users/Amitha/Desktop/NewFolder";	
	String content = "This will be printed in the file and copied to another file. These are numbers to be printed 12 56 78";	
	String Path1 = "C:/Users/Amitha/Desktop/NewFolder/Git1.txt";
	String Path2 = "C:/Users/Amitha/Desktop/NewFolder/Git2.txt";
//	String findFile;


	CreateFolder(folder);
	
	CreateNewFile(Path1);
	
	AddContent(content, Path1);
	
	CopyToFile(Path1, Path2);
	
	DisplayFileContents(Path2);
	
	System.out.println("The folder contents are: ");
	ListFolderContents(folder);
	
	

	 Scanner userIn = new Scanner(System.in);
	 System.out.println("Enter the file to be searched.. " );
	 String findAFile = userIn.next();
	 System.out.println("The path of the file is: ");
	SearchFile(findAFile);
	System.out.println();
	
	
    Scanner scan = new Scanner(System.in);
    System.out.println("Enter the file to be searched.. " );
    String findFile = scan.next();
    System.out.println("Enter the directory where to search ");
	 String newDir = scan.next();
	 String d1 = "C:/Users/Amitha/Desktop/" + newDir;
//	 System.out.println(d1);
	 System.out.println("The path of the file is: ");
    SearchForFile(new File(d1),findFile);
    System.out.println();
	
	
	}
	
	
		/*1. Create a new folder - Takes a parameter of absolute folder path*/
	
	public static void CreateFolder(String CreateF)
	{
		
		File Folder1 = new File(CreateF);
		Folder1.mkdir();
	}
	
	
	
		/*2.Create a new file - Take a parameter of absolute file path*/
		
	public static void CreateNewFile(String CreateFile) throws IOException
	{
		
		String f1 =  "C:/Users/Amitha/Desktop/NewFolder";
		File fnew = new File(f1);
		
		File newFile = new File(CreateFile);
		
		if(fnew.isDirectory())
		{
			if(!newFile.exists())
			{
				newFile.createNewFile();
			}
		}else
			
		{
			
			fnew.mkdir();
		}
	}
	

	
	
	
		/*3. Add content to a file - Take 2 parameters: Content to append to a file; Absolute path to a file*/
	public static void AddContent(String str, String fPath) throws IOException
	{
		File fout = new File(fPath);
		FileOutputStream fs = new FileOutputStream(fout);
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(fs));
		
		
		if(fout.isFile())
		{
			bw.write(str);
			bw.close();
		}
		
		else
		{
			
			System.out.println("File does not exist");
		}
		
	}
	
		
	/* 4. Copy files - Takes 2 parameters: Absolute path to a source file; Absolute path to a destination file (NOTE: If destination file exists, it will be overwritten)*/
	public static void CopyToFile(String srcFile, String desFile) throws IOException
	{
		
		FileReader fr = new FileReader(srcFile);
		BufferedReader br = new BufferedReader(fr);
		String s = null;
		List<String> temp = new ArrayList<String>();
		
		File fout = new File(desFile);
		FileOutputStream fs = new FileOutputStream(fout);
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(fs));
		
				
		while((s = br.readLine())!=null)
		{
			
			temp.add(s); 	
			
		}
		
		for (int i=0; i<temp.size();i++)
		{
			
			bw.write(temp.get(i));
			bw.newLine();
		}
		
		br.close();
		bw.close();
}
	
	
	/* 5.Display file contents - Takes absolute path to a file as an input; Prints out file contents as an output*/
	
	public static void DisplayFileContents(String desFile) throws IOException
	{
		
		FileReader fr = new FileReader(desFile);
		BufferedReader br = new BufferedReader(fr);
		String s = null;
		List<String> temp = new ArrayList<String>();
		
		while((s = br.readLine())!=null)
		{
			
			temp.add(s); 	
			
		}
		
		for (int i=0; i<temp.size();i++)
		{
			
			System.out.println("File Contents are: ");
			System.out.println();
			System.out.println(temp.get(i));
			System.out.println();
			
		}
		
	}

		/* 6.List folder contents - Takes absolute path to a folder as an input; Prints out folder contents as an output*/
		
	public static void ListFolderContents(String nameFolder) throws IOException
	{
		
		    File folderPath = new File(nameFolder);
	        File[] listFiles = folderPath.listFiles();
	        for (File lFiles : listFiles) {
	            if (lFiles.isDirectory()) {
	                System.out.print("Folder:");
	            } else {
	                System.out.print("     file:");
	            }
	            System.out.print(" ");
	            System.out.println(lFiles.getCanonicalPath());
	        }

	}
	
	
		/* 7.Search for a file by name - Takes name of a file to find; Prints out list of absolute paths to files with matching names*/
		
	public static void SearchFile(String srFile)
	{
		
		
		File folder1 = new File("C:/Users/Amitha/Desktop/NewFolder");
		File[] newList = folder1.listFiles();
		
		 if(newList!=null)
	        	
		        for (File fil : newList)
		        {
		        	
		        	if(srFile.equalsIgnoreCase(fil.getName()))
		            {
		                System.out.println(fil.getParentFile());
		                
		            }
		        }
		
		
		
	}
	
	
	/* 8.Search for a file by name - Takes 2 parameters: Absolute path to a starting folder and file name; Outputs list of absolute paths to files with matching names*/
	
	public static void SearchForFile(File searchDir, String sFile)
	{
		
		 
		  	  
		  File[] listCont = searchDir.listFiles();
		 
	        if(listCont!=null)
	        	
	        for (File fil : listCont)
	        {
	        	
//	        	System.out.println(sFile);
//	        	System.out.println(fil.getParentFile());
//	        	System.out.println(fil.getName());
	        	
	            if (fil.isDirectory())
	            {
	            	
//	            	System.out.println(fil);
	            	SearchForFile(fil,sFile);
	            }
	         
	            else if (sFile.equalsIgnoreCase(fil.getName()))
	            {
	                System.out.println(fil.getParentFile());
	                
	            }
	        }
	}
}


