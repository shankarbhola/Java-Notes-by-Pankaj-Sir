[itext PDF](https://www.baeldung.com/java-pdf-creation)

```java
package com.ums.service;

import com.itextpdf.text.*;
import com.itextpdf.text.pdf.PdfWriter;
import org.springframework.stereotype.Service;

import java.io.FileOutputStream;

@Service
public class PDFService {

    public void generateBookingDetailsPDF(){
        try {
            Document document = new Document();
            PdfWriter.getInstance(document, new FileOutputStream("D://booking-confirmation.pdf"));

            document.open();
            Font font = FontFactory.getFont(FontFactory.COURIER, 16, BaseColor.BLACK);
            Chunk chunk = new Chunk("Hello World", font);

            document.add(chunk);
            document.close();
        } catch (Exception e){
            e.printStackTrace();
        }
    }
}

```

```java
@PostMapping("/generatePDF")
    public void generatePDF(){
        pdfService.generateBookingDetailsPDF();
    }
```