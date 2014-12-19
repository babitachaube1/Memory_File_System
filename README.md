Memory_File_System
==================

import java.io.*;
 class  MemoryFileSystem{

public static void main( String[] args){
  InputStream is=null;
  OutputStream os=null;
  String[] files=new String[10];
try{
    //create New folder
 File newDir=new File("C:\\newDir");
 if(!newDir.exists()){
newDir.mkdir();
}
//Create New File
File myFile=new File(newDir,"myFile.txt");
myFile.createNewFile();
//Add content to the file
FileWriter FileWrite=new FileWriter(myFile,true);
BufferedWriter bw=new BufferedWriter(FileWrite);
PrintWriter pw=new PrintWriter(bw);
pw.println("This is a new File for Memory File System");
pw.flush();
pw.close();
File destFile=new File(newDir,"dest.txt");
destFile.createNewFile();
//Copy contents of files from source to destination
        is = new FileInputStream("C:\\newDir\\myFile.txt");
        os = new FileOutputStream("C:\\newDir\\dest.txt");
        byte[] buffer = new byte[1024];
        int length;
        while ((length = is.read(buffer)) > 0) {
            os.write(buffer, 0, length);
        }
        is.close();
    os.close();
   //Display file content 
FileReader fileRead=new FileReader(destFile);
BufferedReader bufferRead=new BufferedReader(fileRead);
while((bufferRead.readLine())!=null){
System.out.println(bufferRead.readLine());
}
bufferRead.close();
//display folder content list files
File search=new File("C:\\newDir");
 files=search.list();
 for(String fn:files){
 System.out.println("found "+fn);
 if(fn.startsWith("myFile")){
     //search for a file by name
     System.out.println("found "+fn);
 }
 }
File[] fileList = getFileList("C:\\newDir");

            for(File file : fileList) {
                System.out.println(file.getName());
            }

}catch(IOException e){}
 
}
//search for a file by name two parameters
 private static File[] getFileList(String dirPath) {
            File dir = new File(dirPath);   

            File[] fileList = dir.listFiles(new FilenameFilter() {
                public boolean accept(File dir, String name) {
                    return name.startsWith("myFile");
                }
            });
            return fileList;
        }
}

