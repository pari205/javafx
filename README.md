# javafx
import java.io.*;
import java.util.zip.*;

public class ZipToDatConverter {
    public static void main(String[] args) {
        // Input zip file and output dat file paths
        String inputZipFilePath = "input.zip";
        String outputDatFilePath = "output.dat";

        try {
            // Create an input stream for the zip file
            FileInputStream fis = new FileInputStream(inputZipFilePath);
            ZipInputStream zipInputStream = new ZipInputStream(new BufferedInputStream(fis));

            // Create an output stream for the dat file
            FileOutputStream fos = new FileOutputStream(outputDatFilePath);
            BufferedOutputStream bos = new BufferedOutputStream(fos);

            byte[] buffer = new byte[1024];
            int bytesRead;

            // Read and write the contents of the zip file to the dat file
            while ((bytesRead = zipInputStream.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesRead);
            }

            // Close streams
            zipInputStream.close();
            bos.close();

            System.out.println("Conversion completed successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


import java.io.*;
import java.util.zip.*;

public class DatToZipConverter {
    public static void main(String[] args) {
        // Input .dat file and output .zip file paths
        String inputDatFilePath = "input.dat";
        String outputZipFilePath = "output.zip";

        try {
            // Create an output stream for the zip file
            FileOutputStream fos = new FileOutputStream(outputZipFilePath);
            ZipOutputStream zipOutputStream = new ZipOutputStream(new BufferedOutputStream(fos));

            // Create an entry in the zip file
            ZipEntry zipEntry = new ZipEntry("data.dat");
            zipOutputStream.putNextEntry(zipEntry);

            // Create an input stream for the .dat file
            FileInputStream fis = new FileInputStream(inputDatFilePath);
            BufferedInputStream bis = new BufferedInputStream(fis);

            byte[] buffer = new byte[1024];
            int bytesRead;

            // Read and write the content of the .dat file to the zip file
            while ((bytesRead = bis.read(buffer)) != -1) {
                zipOutputStream.write(buffer, 0, bytesRead);
            }

            // Close streams
            bis.close();
            zipOutputStream.closeEntry();
            zipOutputStream.close();

            System.out.println("Conversion completed successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
