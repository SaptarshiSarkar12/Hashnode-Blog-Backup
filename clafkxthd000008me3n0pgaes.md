# How to build a File Downloader System

# What is a File Downloader⬇️ System?

A File Downloader System is an application which will download ⬇️ any file 📄 once it is provided with a valid ✅ download link 🔗. In most cases, you can choose the directory 📁 where the file needs to be saved.

# Why build your File Downloader ⬇️ System?

There are tons of file downloading systems either a Web Application🕸️or a desktop application 💻🖥️. Some are free of cost 🆓, but some are paid 💰. Sometimes copyright ©️ marks are also added while downloading any videos 🎥 or documents 📄 if you do not take their premium membership. Ultimately, you depend on those for downloading some files. **What if you make your own File Downloader System?** It will be of course free of cost 🆓 as the services that will be used in this article are open-source and completely free! You can customize the application to run in the way you want. You will learn how those systems work in reality!

# Prerequisites

• Java (Basics) ☕

# Let's Build 🏗️🛠️it!

### 1\. Set Up the project in IDE

I prefer using IntelliJ Idea for this project. You may use your favourite IDE if you wish.

![Project window in IDE](https://cdn.hashnode.com/res/hashnode/image/upload/v1668353094144/z61-dkklM.png align="left")

I have named Project **Drifty**. You may choose any other name.

### 2\. Create the main program

Now, we shall create the main program which includes welcome messages, taking inputs, etc. Create a java source code file (.java) with any name of your choice (I am keeping it Drifty\_CLI.java). Copy the below code to the file you just created.

```java
import java.io.IOException;
import java.net.URL;
import java.util.Objects;
import java.util.Scanner;
/**
 * This is the main class for the CLI version of Drifty.
 */
public class Drifty_CLI {
    private static String downloadsFolder;
    protected static final Scanner SC = new Scanner(System.in);
    public static CreateLogs logger = new CreateLogs("Drifty_CLI_LOG.log");
    public static final String ANSI_RESET = "\u001B[0m";
    public static final String ANSI_CYAN = "\u001B[36m";
    public static final String ANSI_PURPLE = "\u001B[35m";
    private static String fName = null;
    protected static boolean isYoutubeURL;
    public static String versionNumber = "v1.2.2";

    /**
     * This function is the main method of the whole application.
     * @param args Command Line Arguments as a String array.
     */
    public static void main(String[] args) {
        logger.log("INFO", "Application Started !");
        initialPrintBanner();
        if (args.length > 0){
            String URL = args[0];
            String name = null;
            String location = null;
            for (int i = 0; i < args.length; i++){
                if (Objects.equals(args[i], "-help") || Objects.equals(args[i], "-h")){
                    help();
                    System.exit(0);
                } else if (Objects.equals(args[i], "-name") || (Objects.equals(args[i], "-n"))){
                    name = args[i+1];
                } else if (Objects.equals(args[i], "-location") || (Objects.equals(args[i], "-l"))){
                    location = args[i+1];
                } else if (Objects.equals(args[i], "-version") || (Objects.equals(args[i], "-v"))) {
                    System.out.println("Drifty " + versionNumber);
                    System.exit(0);
                }
            }
            if (!isURLValid(URL)) {
                System.out.println("URL is invalid!");
                logger.log("ERROR", "URL is invalid!");
                System.exit(0);
            }
            isYoutubeURL = isYoutubeLink(URL);
            fName = (name==null) ? fName : name;
            if ((fName==null || !containsFilename(URL)) && (!isYoutubeURL)) {
                System.out.print("Enter the filename (with file extension) : ");
                fName = SC.nextLine();
            }
            downloadsFolder = location;
            if (downloadsFolder == null){
                saveToDefault();
            }
            else {
                if (System.getProperty("os.name").contains("Windows")) {
                    downloadsFolder = SC.nextLine().replace('/', '\\');
                    if (!(downloadsFolder.endsWith("\\"))) {
                        downloadsFolder = downloadsFolder + System.getProperty("file.separator");
                    }
                }
            }
            new FileDownloader(URL, fName, downloadsFolder).run();
            System.exit(0);
        }
        while(true) {
            fName = null;
            String link;
            while (true) {
                System.out.print("Enter the link to the file : ");
                link = SC.nextLine();
                isYoutubeURL = isYoutubeLink(link);
                if (isYoutubeURL){
                    break;
                }
                if (!isURLValid(link)) {
                    System.out.println("Invalid URL. Please enter again");
                } else if (!containsFilename(link)) {
                    System.out.println("Automatic file name detection failed!");
                    logger.log("ERROR", "Automatic file name detection failed!");
                    break;
                } else {
                    break;
                }
            }
            System.out.print("Do you want to download the file in your default downloads folder? (Enter Y for yes and N for no) : ");
            String default_folder = SC.nextLine().toLowerCase();
            boolean yesOrNo = yesNoValidation(default_folder, "Do you want to download the file in your default downloads folder? (Enter Y for yes and N for no) : ");
            if (yesOrNo) {
                saveToDefault();
            } else {
                enterDownloadsFolder();
            }
            if (!isYoutubeURL) {
                if (fName != null) {
                    System.out.print("Would you like to rename this file? (Enter Y for yes and N for no) : ");
                    String renameFile = SC.nextLine().toLowerCase();
                    yesOrNo = yesNoValidation(renameFile, "Would you like to rename this file? (Enter Y for yes and N for no) : ");
                    if (yesOrNo) {
                        System.out.print("Enter the filename (with file extension) : ");
                        fName = SC.nextLine();
                    }
                } else {
                    System.out.print("Enter the filename (with file extension) : ");
                    fName = SC.nextLine();
                }
            }
            new FileDownloader(link, fName, downloadsFolder).run();
            System.out.println("Press Q to Quit Or Press any Key to Continue");
            String quit = SC.nextLine().toLowerCase();
            if(quit.equals("q")){
                logger.log("INFO", "Application Terminated!");
                break;
            }
            printBanner();
        }
    }

    /**
     * This function takes a folder path as input from the user, where the file will be saved.
     */
    private static void enterDownloadsFolder(){
        System.out.print("Enter the directory in which you want to download the file : ");
        downloadsFolder = SC.nextLine();
        if (System.getProperty("os.name").contains("Windows")) {
            downloadsFolder = SC.nextLine().replace('/', '\\');
            if (!(downloadsFolder.endsWith("\\"))) {
                downloadsFolder = downloadsFolder + System.getProperty("file.separator");
            }
        }
        logger.log("INFO", "Custom Directory Entered : " + downloadsFolder);
    }

    /**
     * This function tries to detect the default downloads folder and save the file in that folder
     */
    private static void saveToDefault(){
        System.out.println("Trying to auto-detect default Downloads folder...");
        logger.log("INFO", "Trying to auto-detect default Downloads folder...");
        if (!System.getProperty("os.name").contains("Windows")) {
            String home = System.getProperty("user.home");
            downloadsFolder = home + "/Downloads/";
        }
        else {
            downloadsFolder = DefaultDownloadFolderLocationFinder.findPath() + System.getProperty("file.separator");
        }
        if (downloadsFolder.equals(System.getProperty("file.separator")) || downloadsFolder == null) {
            System.out.println("Failed to retrieve default download folder!");
            logger.log("ERROR", "Failed to retrieve default download folder!");
            enterDownloadsFolder();
        } else {
            System.out.println("Default download folder detected : " + downloadsFolder);
            logger.log("INFO", "Default download folder detected : " + downloadsFolder);
        }
    }

    /**
     * @param link Link to the file that the user wants to download
     * @return true if link is valid and false if link is invalid
     */
    private static boolean isURLValid(String link){
        try{
            new URL(link).toURI();
            return true;
        }
        catch (Exception e){
            return false;
        }
    }

    /**
     * This method checks whether the link provided is of YouTube or not and returns the resultant boolean value accordingly.
     * @param url link to the file to be downloaded.
     * @return true if the url is of YouTube and false if it is not.
     */
    public static boolean isYoutubeLink(String url) {
        String pattern = "^(http(s)?:\\/\\/)?((w){3}.)?youtu(be|.be)?(\\.com)?\\/.+";
        return url.matches(pattern);
    }

    /**
     * @param link Link to the file that the user wants to download
     * @return true if the filename is detected and false if the filename is not detected
     */
    private static boolean containsFilename(String link){
        // Check and inform user if the url contains filename.
        // Example : "example.com/file.txt" prints "Filename detected: file.txt"
        // example.com/file.json -> file.json
        String file = link.substring(link.lastIndexOf("/")+1);
        int index = file.lastIndexOf(".");
        if (index < 0 || index > file.length()){
            return false;
        }
        String extension = file.substring(index);
        // edge case 1 : "example.com/."
        if (extension.length()==1){
            return false;
        }
        // file.png?width=200 -> file.png
        fName = file.split("([?])")[0];
        System.out.println("Filename detected : " + fName);
        logger.log("INFO", "Filename detected : " + fName);
        return true;
    }

    /**
     * This method performs Yes-No validation and returns the boolean value accordingly.
     * @param input Input String to validate.
     * @param printMsg The message to print to re-input the confirmation.
     * @return true if the user enters Y [Yes] and false if not.
     */
    public static boolean yesNoValidation(String input, String printMsg){
        while (true) {
            if (input.length() == 0) {
                System.out.println("Please enter Y for yes and N for no!");
                logger.log("ERROR", "Please enter Y for yes and N for no!");
            } else {
                break;
            }
            System.out.print(printMsg);
            input = SC.nextLine().toLowerCase();
        }
        char choice = input.charAt(0);
        if (choice == 'y') {
            return true;
        } else if (choice =='n'){
            return false;
        }
        else {
            System.out.println("Invalid input!");
            logger.log("ERROR", "Invalid input");
            System.out.print(printMsg);
            input = SC.nextLine().toLowerCase();
            yesNoValidation(input, printMsg);
        }
        return false;
    }

    /**
     * This function provides help about how to use the application through command line arguments.
     */
    private static void help(){
        System.out.println(ANSI_RESET+"\n\033[38;31;48;40;1m----==| DRIFTY CLI HELP |==----"+ANSI_RESET);
        System.out.println("\033[38;31;48;40;0m            v1.2.2"+ANSI_RESET);
        System.out.println("For more information visit: https://github.com/SaptarshiSarkar12/Drifty/");
        System.out.println("\033[31;1mRequired parameter: File URL"+ANSI_RESET+" \033[3m(This must be the first argument you are passing)"+ANSI_RESET);
        System.out.println("\033[33;1mOptional parameters:");
        System.out.println("\033[97;1mName        ShortForm     Default     Description"+ANSI_RESET);
        System.out.println("-location   -l            Downloads                   The location on your computer where content downloaded from Drifty are placed.");
        System.out.println("-name       -n            Source                      Renames file.");
        System.out.println("-help       -h            N/A                         Provides concise information for Drifty CLI.\n");
        System.out.println("-version    -v            Current Version Number      Displays version number of Drifty.");
        System.out.println("\033[97;1mExample:" + ANSI_RESET + " \n> \033[37;1mjava Drifty_CLI https://example.com/object.png -n obj.png -l C:/Users/example"+ ANSI_RESET );
        System.out.println("\033[37;3m* Requires java 18 or higher. \n"+ANSI_RESET);
    }

    /**
     * This function prints the banner of the application in the console.
     */
    private static void printBanner(){
        System.out.print("\033[H\033[2J");
        System.out.println(ANSI_PURPLE+"===================================================================="+ANSI_RESET);
        System.out.println(ANSI_CYAN+"  _____   _____   _____  ______  _______ __     __"+ANSI_RESET);
        System.out.println(ANSI_CYAN+" |  __ \\ |  __ \\ |_   _||  ____||__   __|\\ \\   / /"+ANSI_RESET);
        System.out.println(ANSI_CYAN+" | |  | || |__) |  | |  | |__      | |    \\ \\_/ /"+ANSI_RESET);
        System.out.println(ANSI_CYAN+" | |  | ||  _  /   | |  |  __|     | |     \\   / "+ANSI_RESET);
        System.out.println(ANSI_CYAN+" | |__| || | \\ \\  _| |_ | |        | |      | |  "+ANSI_RESET);
        System.out.println(ANSI_CYAN+" |_____/ |_|  \\_\\|_____||_|        |_|      |_|  "+ANSI_RESET);
        System.out.println(ANSI_PURPLE+"===================================================================="+ANSI_RESET);
    }

    /**
     * This method prints the banner without any colour of text except white.
     */
    private static void initialPrintBanner(){
        System.out.println("====================================================================");
        System.out.println("  _____   _____   _____  ______  _______ __     __");
        System.out.println(" |  __ \\ |  __ \\ |_   _||  ____||__   __|\\ \\   / /");
        System.out.println(" | |  | || |__) |  | |  | |__      | |    \\ \\_/ /");
        System.out.println(" | |  | ||  _  /   | |  |  __|     | |     \\   / ");
        System.out.println(" | |__| || | \\ \\  _| |_ | |        | |      | |  ");
        System.out.println(" |_____/ |_|  \\_\\|_____||_|        |_|      |_|  ");
        System.out.println("====================================================================");
    }
}
```

We have used the Scanner class to take input from the user, the URL class to convert the link from String to an URL 🔗, IOException class to handle IO Exceptions, and Objects class for command line arguments' handling. Some ANSI Colour Codes are also used to make the Application visually more appealing. Appropriate inputs and their validations are performed. Also, a help command is kept for more information on the Application.

### 3\. Creating the program to Download ⬇️ the file 📄

Now, we shall look into the core part of the whole project which is the downloading part --- How to download the file? How to save it? Create a FileDownloader.java class and copy the below code to that class.

```plaintext
import java.io.*;
import java.net.*;
import java.nio.channels.Channels;
import java.nio.channels.ReadableByteChannel;
import java.util.ArrayList;
import java.util.List;

/**
 * This class deals with downloading the file.
 */
class FileDownloader implements Runnable {
    private static String dir;
    private static String fileName;
    private static String link;
    private static long totalSize;
    private static URL url;
    private static boolean supportsMultithreading;
    // default number of threads to download with
    private final static int numberOfThreads = 3;
    // default threading threshold in bytes  50MB
    private final static long threadingThreshold = 1024 * 1024 * 50;

    /**
     * This is a constructor to initialise values of link, fileName and dir variables.
     *
     * @param link     Link to the file that the user wants to download
     * @param fileName Filename of the file that the user wants to save as after it is downloaded
     * @param dir      Directory in which the file needs to be saved.
     */
    public FileDownloader(String link, String fileName, String dir) {
        FileDownloader.link = link;
        FileDownloader.fileName = fileName;
        FileDownloader.dir = dir;
        FileDownloader.supportsMultithreading = false;
    }

    /**
     * This function is used to get the value of dir variable.
     *
     * @return The directory in which the user wants to save the file.
     */
    public static String getDir() {
        return dir;
    }

    /**
     * This is the overridden run method of the Runnable interface and deals with the main part of opening connections and downloading the file.
     */
    @Override
    public void run() {
        link = link.replace('\\', '/');
        if (!(link.startsWith("http://") || link.startsWith("https://"))) {
            link = "http://" + link;
        }
        if (link.startsWith("https://github.com/") || (link.startsWith("http://github.com/"))) {
            if (!(link.endsWith("?raw=true"))) {
                link = link + "?raw=true";
            }
        }
        try {
            // If link is of an YouTube video, then the following block of code will execute.
            if (Drifty_CLI.isYoutubeLink(link)) {
                try {
                    downloadFromYouTube("");
                } catch (IOException e) {
                    try {
                        System.out.println("Getting ready to download the file...");
                        Drifty_CLI.logger.log("INFO", "Getting ready to download the file...");
                        copyYt_dlp cy = new copyYt_dlp();
                        cy.copyToTemp();
                        try {
                            downloadFromYouTube(copyYt_dlp.tempDir);
                        } catch (InterruptedException ie) {
                            System.out.println("User interrupted while downloading the file!");
                            Drifty_CLI.logger.log("ERROR", "User interrupted while downloading the file! " + ie.getMessage());
                        } catch (IOException io1) {
                            System.out.println("Failed to download YouTube video!");
                            Drifty_CLI.logger.log("ERROR", "Failed to download YouTube video! " + io1.getMessage());
                        }
                    } catch (IOException io) {
                        System.out.println("Failed to initialise YouTube video downloader!");
                        Drifty_CLI.logger.log("ERROR", "Failed to initialise YouTube video downloader! " + io.getMessage());
                    }
                } catch (InterruptedException e) {
                    System.out.println("User interrupted while downloading the file!");
                    Drifty_CLI.logger.log("ERROR", "User interrupted while downloading the file! " + e.getMessage());
                }
            } else {
                url = new URL(link);
                URLConnection openConnection = url.openConnection();
                openConnection.connect();
                totalSize = openConnection.getHeaderFieldLong("Content-Length", -1);

                String acceptRange = openConnection.getHeaderField("Accept-Ranges");
                FileDownloader.supportsMultithreading = totalSize > threadingThreshold && acceptRange != null && acceptRange.equalsIgnoreCase("bytes");

                if (fileName.length() == 0) {
                    String[] webPaths = url.getFile().trim().split("/");
                    fileName = webPaths[webPaths.length - 1];
                }
                dir = dir.replace('/', '\\');
                if (dir.length() != 0) {
                    if (dir.equals(".\\\\") || dir.equals(".\\")) {
                        dir = "";
                    }
                } else {
                    System.out.println("Invalid Directory Entered !");
                    Drifty_CLI.logger.log("ERROR", "Invalid Directory Entered !");
                }
                try {
                    new CheckDirectory(dir);
                } catch (IOException e) {
                    System.out.println("Failed to create the directory : " + dir + " ! " + e.getMessage());
                    Drifty_CLI.logger.log("ERROR", "Failed to create the directory : " + dir + " ! " + e.getMessage());
                }
                System.out.println("Trying to download the file...");
                Drifty_CLI.logger.log("INFO", "Trying to download the file...");
                downloadFile();
            }
        } catch (MalformedURLException e) {
            System.out.println("Invalid Link!");
            Drifty_CLI.logger.log("ERROR", "Invalid Link! " + e.getMessage());
        } catch (SocketTimeoutException e) {
            System.out.println("Timed out while connecting to " + url + " !");
            Drifty_CLI.logger.log("ERROR", "Timed out while connecting to " + url + " ! " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Failed to connect to " + url + " !");
            Drifty_CLI.logger.log("ERROR", "Failed to connect to " + url + " ! " + e.getMessage());
        }
    }

    /**
     * This method deals with downloading the file.
     */
    private static void downloadFile() {
        try {
            ReadableByteChannel readableByteChannel;
            try {
                if (FileDownloader.supportsMultithreading) {

                    List<FileOutputStream> fileOutputStreams = new ArrayList<>(FileDownloader.numberOfThreads);
                    List<Long> partSizes = new ArrayList<>(FileDownloader.numberOfThreads);
                    List<File> tempFiles = new ArrayList<>(FileDownloader.numberOfThreads);
                    List<DownloaderThread> downloaderThreads = new ArrayList<>(FileDownloader.numberOfThreads);
                    long partSize = Math.floorDiv(totalSize, FileDownloader.numberOfThreads);
                    long start, end;
                    FileOutputStream fileOut;
                    File file;
                    for (int i = 0; i < FileDownloader.numberOfThreads; i++) {
                        file = File.createTempFile(fileName.hashCode() + "" + i, ".tmp");
                        fileOut = new FileOutputStream(file);
                        start = i == 0 ? 0 : (i * partSize) + 1;
                        end = FileDownloader.numberOfThreads - 1 == i ? totalSize : ((i * partSize) + partSize);
                        DownloaderThread downloader = new DownloaderThread(url, fileOut, start, end);
                        downloader.start();
                        fileOutputStreams.add(fileOut);
                        partSizes.add(end - start);
                        downloaderThreads.add(downloader);
                        tempFiles.add(file);
                    }

                    ProgressBarThread progressBarThread = new ProgressBarThread(fileOutputStreams, partSizes, fileName);
                    progressBarThread.start();
                    //check if all file are downloaded
                    try {
                        while (!merge(fileOutputStreams, partSizes, downloaderThreads, tempFiles)) {
                            Thread.sleep(1000);
                        }
                        progressBarThread.setDownloading(false);
                        // keep main thread from closing the IO for short amt. of time so UI thread can finish and output
                        try {
                            Thread.sleep(1000);
                        } catch (InterruptedException ignored) {}
                    } catch (InterruptedException ignored) {
                    }
                } else {

                    InputStream urlStream = url.openStream();
                    System.out.println();
                    readableByteChannel = Channels.newChannel(urlStream);

                    FileOutputStream fos = new FileOutputStream(dir + fileName);
                    ProgressBarThread progressBarThread = new ProgressBarThread(fos, totalSize, fileName);
                    progressBarThread.start();
                    Drifty_CLI.logger.log("INFO", "Downloading " + fileName + " ...");
                    fos.getChannel().transferFrom(readableByteChannel, 0, Long.MAX_VALUE);
                    progressBarThread.setDownloading(false);
                    // keep main thread from closing the IO for short amt. of time so UI thread can finish and output
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException ignored) {
                    }
                }

            } catch (SecurityException e) {
                System.out.println("Write access to " + dir + fileName + " denied !");
                Drifty_CLI.logger.log("ERROR", "Write access to " + dir + fileName + " denied ! " + e.getMessage());
            } catch (IOException e) {
                System.out.println("Failed to download the contents ! ");
                Drifty_CLI.logger.log("ERROR", "Failed to download the contents ! " + e.getMessage());
            }
        } catch (NullPointerException e) {
            System.out.println("Failed to get I/O operations channel to read from the data stream !");
            Drifty_CLI.logger.log("ERROR", "Failed to get I/O operations channel to read from the data stream !" + e.getMessage());
        }
        if (dir.length() == 0) {
            dir = System.getProperty("user.dir");
        }
        if (!(dir.endsWith("\\"))) {
            dir = dir + System.getProperty("file.separator");
        }

    }

    /**
     * This method deals with downloading videos from YouTube in mp4 format.
     *
     * @param dirOfYt_dlp The directory of yt-dlp file. Default - "". If Drifty is run from its jar file, this argument will have the directory where yt-dlp has been extracted to (the temporary files' folder).
     * @throws InterruptedException When the I/O operation is interrupted using keyboard or such type of inputs.
     * @throws IOException          When an I/O problem appears while downloading the YouTube video.
     */
    private static void downloadFromYouTube(String dirOfYt_dlp) throws InterruptedException, IOException {
        String fName = "";
        System.out.println("Trying to auto-detect filename...");
        ProcessBuilder processBuilder = new ProcessBuilder(dirOfYt_dlp + "yt-dlp", link, "--print", "title");
        processBuilder.inheritIO();
        System.out.print("Filename : ");
        Process yt_dlp = processBuilder.start();
        yt_dlp.waitFor();
        int exitValueOfYt_Dlp = yt_dlp.exitValue();
        if (exitValueOfYt_Dlp != 0){
            return;
        }
        System.out.print("Would you like to rename this file? (Enter Y for yes and N for no) : ");
        String renameFile = Drifty_CLI.SC.nextLine().toLowerCase();
        boolean yesOrNo = Drifty_CLI.yesNoValidation(renameFile, "Would you like to rename this file? (Enter Y for yes and N for no) : ");
        if (yesOrNo) {
            System.out.print("Enter the filename (with file extension) : ");
            fName = Drifty_CLI.SC.nextLine();
        }
        System.out.println("Trying to download the file ...");
        Drifty_CLI.logger.log("INFO", "Trying to download the file ...");
        if (fName.equals("")){
            processBuilder = new ProcessBuilder(dirOfYt_dlp + "yt-dlp", "--quiet", "--progress", "-P", dir, link, "-o", "%(title)s.mp4");
        } else {
            processBuilder = new ProcessBuilder(dirOfYt_dlp + "yt-dlp", "--quiet", "--progress", "-P", dir, link, "-o", fName);
        }
        processBuilder.inheritIO();
        yt_dlp = processBuilder.start();
        yt_dlp.waitFor();
        exitValueOfYt_Dlp = yt_dlp.exitValue();
        if (exitValueOfYt_Dlp == 0) {
            System.out.println("Successfully downloaded the file!");
            Drifty_CLI.logger.log("INFO", "Successfully downloaded the file!");
        } else if (exitValueOfYt_Dlp == 1) {
            System.out.println("Failed to download the file!");
            Drifty_CLI.logger.log("INFO", "Failed to download the file!");
        }
    }

    /**
     * This method check if all the downloader threads are completed correctly and merges the downloaded parts.
     * @param fileOutputStreams FileOutputStream of all the parts
     * @param partSizes         Size each of the parts
     * @param downloaderThreads DownloaderThreads of all the parts
     * @param tempFiles         Temporary files containing the parts
     * @return true if merge is successful and false if the file is still being downloaded
     * @throws IOException if the threads exit without downloading the whole part or if there are any IO error thrown by  getChannel().size() method of FileOutputStream
     */
    public static boolean merge(List<FileOutputStream> fileOutputStreams, List<Long> partSizes, List<DownloaderThread> downloaderThreads, List<File> tempFiles) throws IOException {
        //check if all file are downloaded
        int completed = 0;
        FileOutputStream fout;
        DownloaderThread downloaderThread;
        long partSize;
        for (int i = 0; i < FileDownloader.numberOfThreads; i++) {
            fout = fileOutputStreams.get(i);
            partSize = partSizes.get(i);
            downloaderThread = downloaderThreads.get(i);

            if (fout.getChannel().size() < partSize) {
                if (!downloaderThread.isAlive())
                    throw new IOException("Error: thread encountered an error");
            } else if (!downloaderThread.isAlive())
                completed++;
        }

        //check if it is merge-able
        if (completed == FileDownloader.numberOfThreads) {
            fout = new FileOutputStream(dir + fileName);
            long position = 0;
            for (int i = 0; i < FileDownloader.numberOfThreads; i++) {
                File f = tempFiles.get(i);
                FileInputStream fs = new FileInputStream(f);
                ReadableByteChannel rbs = Channels.newChannel(fs);
                fout.getChannel().transferFrom(rbs, position, f.length());
                position += f.length();
            }
            fout.close();
            return true;
        }
        return false;
    }
}
```

```plaintext
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URL;
import java.net.URLConnection;
import java.nio.channels.Channels;
import java.nio.channels.ReadableByteChannel;

public class DownloaderThread extends Thread{

    private URL url;
    private FileOutputStream file;
    private long start;
    private long end;

    public DownloaderThread(URL url, FileOutputStream file, long start, long end) {
        this.url=url;
        this.file = file;
        this.start = start;
        this.end = end;
    }

    @Override
    public void run() {
        ReadableByteChannel readableByteChannel;
        try {
            URLConnection con = url.openConnection();
            con.setRequestProperty("Range", "bytes="+start+"-"+end);
            con.connect();
            readableByteChannel = Channels.newChannel(con.getInputStream());
            file.getChannel().transferFrom(readableByteChannel, 0, Long.MAX_VALUE);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

Here, we have used the io package to handle the input and output, Channels and ReadableByteChannel to get a network channel through which the bytes of data can be received, ArrayList to store the temporary files 📄, size of the part of the file to be downloaded and the download ⬇️ threads. This class is a thread and multithreaded downloading mechanism is implemented which makes downloading faster 🚀🚀!!

### 4\. Adding a Progress Bar

The main part of the project has been completed, now, we shall look into introducing a progress bar to indicate how much has been downloaded and how much is left. Create ProgressBarThread.java class and copy the below code.

```plaintext
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

/**
 * This is the class responsible for showing the progress bar in the console.
 */
public class ProgressBarThread extends Thread {
    private final float charPercent;
    private long downloadedBytes;
    private List<Long> downloadedBytesPerPart;
    private boolean downloading;
    private long downloadSpeed;
    private List<Long> downloadSpeeds;
    private final List<Long> partSizes;
    private final String fileName;
    private final FileOutputStream fos;
    private long totalDownloadBytes;
    private final int charAmt;
    private final List<Integer> charPercents;
    private final List<FileOutputStream> fileOutputStreams;
    private final boolean isThreadedDownloading;

    public ProgressBarThread(List<FileOutputStream> fileOutputStreams, List<Long> partSizes, String fileName) {
        this.partSizes = partSizes;
        this.fileName = fileName;
        this.fileOutputStreams = fileOutputStreams;
        charPercent = 0;
        fos = null;
        totalDownloadBytes = 0;
        charAmt = 80/fileOutputStreams.size();
        isThreadedDownloading = true;
        downloading = true;
        charPercents = new ArrayList<>(fileOutputStreams.size());
        downloadedBytesPerPart = new ArrayList<>(fileOutputStreams.size());
        downloadSpeeds = new ArrayList<>(fileOutputStreams.size());
        for (int i = 0; i < fileOutputStreams.size(); i++) {
            charPercents.add((int) (partSizes.get(i) / charAmt));
        }
    }

    /**
     * Progress Bar Constructor to initialise data members.
     *
     * @param fos                Output stream for writing contents from the web to the local file.
     * @param totalDownloadBytes Total size of the file in bytes.
     * @param fileName           Filename of the downloaded file.
     */
    public ProgressBarThread(FileOutputStream fos, long totalDownloadBytes, String fileName) {
        this.charAmt = 20; // value to determine length of terminal progressbar
        this.downloading = true;
        this.downloadSpeed = 0;
        this.downloadedBytes = 0;
        this.totalDownloadBytes = totalDownloadBytes;
        this.fileName = fileName;
        this.fos = fos;
        this.charPercent = (int) (this.totalDownloadBytes / charAmt);

        fileOutputStreams = null;
        partSizes = null;
        isThreadedDownloading = false;
        charPercents = null;
    }

    /**
     * @param downloading true if the file is being downloaded and false if it's not.
     */
    public void setDownloading(boolean downloading) {
        this.downloading = downloading;
        if (downloading) {
            System.out.println("Downloading " + fileName + " ...");
        }
    }

    /**
     * Generates progress bar.
     *
     * @param spinner icon
     * @return String object containing the progress bar.
     */
    private String generateProgressBar(String spinner) {
        if (!isThreadedDownloading) {
            float filled = downloadedBytes / charPercent;
            String a = new String(new char[(int) filled]).replace("\0", "=");
            String b = new String(new char[charAmt - (int) filled]).replace("\0", ".");
            String bar = a + b;
            bar = bar.substring(0, charAmt / 2 - 2) + String.format("%02d", (int) (downloadedBytes * 100 / totalDownloadBytes)) + "%" + bar.substring(charAmt / 2 + 1);
            return "[" + spinner + "]  " + fileName + "  (0KB)[" + bar + "](" + convertBytes(totalDownloadBytes) + ")  " + (float) downloadSpeed / 1000000 + " MB/s      ";
        } else {
            String result = "[" + spinner + "]  "+ convertBytes(totalDownloadBytes) ;
            float filled;
            totalDownloadBytes=0;
            for (int i = 0; i < fileOutputStreams.size(); i++) {
                filled = downloadedBytesPerPart.get(i) / ((float) charPercents.get(i));
                totalDownloadBytes += downloadedBytesPerPart.get(i);
                String a = new String(new char[(int) filled]).replace("\0", "=");
                String b = new String(new char[charAmt - (int) filled]).replace("\0", ".");
                String bar = a + b;
                bar = bar.substring(0, charAmt / 2 - 2) + String.format("%02d", (int) (downloadedBytesPerPart.get(i) * 100 / partSizes.get(i))) + "%" + bar.substring(charAmt / 2 + 1);
                result += " [" + bar + "] " + String.format("%.2f",(float) downloadSpeeds.get(i) / 1000000) + " MB/s";
            }
            return result;
        }
    }

    /**
     * @param bytes file size in bytes.
     * @return returns a String object containing the file size with proper units.
     */
    private String convertBytes(long bytes) {
        String sizeWithUnit;
        double bytesWithDecimals;
        if (bytes > 1024) {
            bytesWithDecimals = bytes / 1024.0;
            sizeWithUnit = String.format("%.2f", bytesWithDecimals)  + " KB";
            if (bytesWithDecimals > 1024) {
                bytesWithDecimals = bytesWithDecimals / 1024;
                sizeWithUnit = String.format("%.2f",bytesWithDecimals)  + " MB";
                if (bytesWithDecimals > 1024) {
                    bytesWithDecimals = bytesWithDecimals / 1024;
                    sizeWithUnit = String.format("%.2f",bytesWithDecimals) + "GB";
                }
            }
            return sizeWithUnit;
        } else {
            return totalDownloadBytes + " bytes";
        }
    }

    /**
     * Cleans up the resources.
     */
    private void cleanup() {
        System.out.println("\r" + generateProgressBar("/"));
        if(isThreadedDownloading){
            String sizeWithUnit = convertBytes(totalDownloadBytes);
            System.out.println("Downloaded " + fileName + " of size " + sizeWithUnit + " at " + FileDownloader.getDir() + fileName + " successfully !");
            Drifty_CLI.logger.log("INFO", "Downloaded " + fileName + " of size " + sizeWithUnit + " at " + FileDownloader.getDir() + fileName + " successfully !");
        }else if (downloadedBytes == totalDownloadBytes) {
            String sizeWithUnit = convertBytes(downloadedBytes);
            System.out.println("Downloaded " + fileName + " of size " + sizeWithUnit + " at " + FileDownloader.getDir() + fileName + " successfully !");
            Drifty_CLI.logger.log("INFO", "Downloaded " + fileName + " of size " + sizeWithUnit + " at " + FileDownloader.getDir() + fileName + " successfully !");
        } else {
            System.out.println("Download failed!");
            Drifty_CLI.logger.log("ERROR", "Download failed!");
        }
    }

    /**
     * run method for progress bar.
     */
    @Override
    public void run() {
        long initialMeasurement;
        String[] spinner = new String[]{"/", "-", "\\", "|"};
        List<Long> initialMeasurements = isThreadedDownloading ? new ArrayList<>(fileOutputStreams.size()) : null;
        while (downloading) {
            try {
                if (!isThreadedDownloading) {
                    for (int i = 0; i <= 3; i++) {
                        initialMeasurement = fos.getChannel().size();
                        Thread.sleep(250);
                        downloadedBytes = fos.getChannel().size();
                        downloadSpeed = (downloadedBytes - initialMeasurement) * 4;
                        System.out.print("\r" + generateProgressBar(spinner[i]));
                    }
                } else {
                    for (int i = 0; i <= 3; i++) {
                        for (int j = 0; j < fileOutputStreams.size(); j++) {
                            initialMeasurements.add(j,fileOutputStreams.get(j).getChannel().size());
                        }
                        Thread.sleep(300);
                        long downloadedPartBytes;
                        for (int j = 0; j < fileOutputStreams.size(); j++) {
                            downloadedPartBytes = fileOutputStreams.get(j).getChannel().size();
                            downloadedBytesPerPart.add(j,downloadedPartBytes);
                            downloadSpeeds.add(j, (downloadedPartBytes - initialMeasurements.get(j)) * 4);
                        }
                        System.out.print("\r" + generateProgressBar(spinner[i]));
                    }
                }
            } catch (InterruptedException | IOException ignored) {
            }
        }
        cleanup();
    }
}
```

We have made this class as a thread. The **generateProgressBar** method generates a string corresponding to the download ⬇️ progress and it is then printed in the console.

### 5\. Some other features 💡💡

Here is the source code of some other features that you may include to make the application more feature intensive.

```plaintext
import java.io.File;
import java.io.IOException;
import java.nio.file.FileSystems;
import java.nio.file.Files;
import java.nio.file.Path;

/**
 * This class checks if a directory exists or not. if it doesn't, the directory is created.
 */
class CheckDirectory {
    /**
     * This constructor creates the directory if it does not exist.
     * @param dir Name of the folder where the user wants to download the file.
     * @throws IOException when creating the directory fails.
     */
    CheckDirectory(String dir) throws IOException {
        if (!(checkIfFolderExists(dir))){
            Path directory = FileSystems.getDefault().getPath(dir);
            Files.createDirectory(directory);
            Drifty_CLI.logger.log("INFO", "Directory Created");
        }
    }

    /**
     * This function checks if a folder exists or not.
     * @param folderName Name of the folder where the user wants to download the file.
     * @return true if the folder exists and false if the folder is missing.
     */
    private static boolean checkIfFolderExists(String folderName) {
        boolean found = false;
        try {
            File file = new File(folderName);
            if (file.exists() && file.isDirectory()) {
                found = true;
            }
        } catch (Exception e) {
            System.out.println("Error while checking for directory !");
            Drifty_CLI.logger.log("ERROR", "Error while checking for directory !");
        }
        return found;
    }
}
```

The above code tries to validate if the custom download directory 📂 exists or not. If it does not exist, the new directory 📂 will be created. Exceptions are handled 🛠️ and appropriate messages 🗯️ are shown.

```plaintext
import java.io.*;

/**
 * This class deals with finding the path of the default downloads folder.
 */
class DefaultDownloadFolderLocationFinder {
    private static final String REG_TOKEN = "REG_EXPAND_SZ";

    /**
     * This function finds the path of the default downloads folder.
     * @return The path of the default downloads folder as a String object.
     */
    public static String findPath() {
        try {
            Process process = new ProcessBuilder("reg", "query", "\"HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\User Shell Folders\"", "/v", "{374DE290-123F-4565-9164-39C4925E467B}").start();
            StreamReader reader = new StreamReader(process.getInputStream());
            reader.start();
            process.waitFor();
            reader.join();
            String result = reader.getResult();
            int p = result.indexOf(REG_TOKEN);
            if (p == -1) {
                return null;
            }

            result = result.substring(p + REG_TOKEN.length()).trim();
            result = result.replace("%USERPROFILE%", System.getProperty("user.home"));

            return result;
        }
        catch (Exception e) {
            return null;
        }
    }
    static class StreamReader extends Thread {
        private final InputStream is;
        private final StringWriter sw;

        StreamReader(InputStream is) {
            this.is = is;
            sw = new StringWriter();
        }

        @Override
        public void run() {
            try {
                int c;
                while ((c = is.read()) != -1)
                    sw.write(c);
            }
            catch (IOException ignored) {

            }
        }
        public String getResult() {
            return sw.toString();
        }
    }
}
```

The above code tries to detect the default downloads folder 📂. If it fails to detect, then the main program made in 2nd step is going to take the custom download folder 📂 as input.

```plaintext
import java.io.*;
import java.nio.file.FileSystems;
import java.nio.file.Path;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;

/**
 * This class deals with creating Log files for Drifty.
 */
public class CreateLogs {
    static DateFormat df;
    static boolean isLogEmpty;
    static Path filePath;
    static Calendar calObj = Calendar.getInstance();

    /**
     * This is the constructor used to initialise the variables in this class.
     * @param logFileName Filename of the Log file.
     */
    public CreateLogs(String logFileName){
        filePath = FileSystems.getDefault().getPath(logFileName);
        df = new SimpleDateFormat("dd-MMM-yyyy HH:mm:ss");
    }

    /**
     * This function actually writes the entries to the log file.
     * @param type Type of the Log (acceptable values - INFO, WARN, ERROR).
     * @param msg Log message.
     */
    public void log(String type, String msg){
        String dateAndTime = df.format(calObj.getTime());
        if (!isLogEmpty){
            clearLog();
        }
        try (PrintWriter out = new PrintWriter(new BufferedWriter(new OutputStreamWriter(new FileOutputStream("Drifty_CLI_LOG.log", true))))) {
            isLogEmpty = true;
            out.println(dateAndTime + " " + type.toUpperCase() + " - " + msg);
        } catch (IOException e) {
            System.out.println("Failed to create log : " + msg);
        }
    }

    /**
     * This function clears the contents of the previous log file.
     */
    private static void clearLog(){
        try (PrintWriter out = new PrintWriter(new BufferedWriter(new OutputStreamWriter(new FileOutputStream("Drifty_CLI_LOG.log", false))))) {
            isLogEmpty = true;
            out.write("");
        } catch (IOException e) {
            System.out.println("Failed to clear Log contents !");
            Drifty_CLI.logger.log("ERROR", "Failed to clear Log contents !");
        }
    }
}
```

The above code is used to store Logs 📃 of the Application in a file 📁 (Here, I have kept the name as Drifty\_CLI\_LOG.log). You may keep any other name also.

```plaintext
import java.io.FileOutputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class copyYt_dlp {
    public static final String tempDir = System.getProperty("java.io.tmpdir");
    public void copyToTemp() throws IOException{
        File file = new File(tempDir + "yt-dlp.exe");
        if (file.exists()){
            Drifty_CLI.logger.log("INFO", "Skipping copying yt-dlp to " + tempDir + " folder as it is already present!");
            return;
        }
        InputStream is = getClass().getResource("yt-dlp.exe").openStream();
        // sets the output stream to a system folder
        OutputStream os = new FileOutputStream(System.getProperty("java.io.tmpdir") + "yt-dlp.exe");
        byte[] b = new byte[2048]; // length of the byte array doesn't matter in copying the file to the temp folder!
        int length;
        while ((length = is.read(b)) != -1) {
            os.write(b, 0, length);
        }
        is.close();
        os.close();
    }
}
```

The above code is helpful when the whole project is converted and used as a Jar file🫙. The code basically moves the yt\_dlp.exe program responsible for downloading ⬇️ a YouTube video 🎥 to a temporary directory, thus, preventing the application from crashing💥. You need to download [yt\_dlp program](https://github.com/yt-dlp/yt-dlp) for your OS to download YouTube videos using this Application we just made.

### And We are done!! 🚀🚀 Our Application is running!!

The source codes can be found in [this GitHub repository](https://github.com/SaptarshiSarkar12/Drifty). For any problem or issues, you may [contact me here](https://bio.link/saptarshi). Please leave a star ⭐ on the repository if you liked it. Thanks to all the contributors who have contributed to this project!! The project also has a [website](https://saptarshisarkar12.github.io/Drifty/). You may have a visit.

## Thank You!