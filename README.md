import PyPDF2
   from googletrans import Translator
   from reportlab.lib.pagesizes import letter
   from reportlab.pdfgen import canvas

   def translate_pdf(input_path, output_path, src_lang='en', dest_lang='uz'):
       pdf_reader = PyPDF2.PdfFileReader(input_path)
       translator = Translator()

       c = canvas.Canvas(output_path, pagesize=letter)

       for page_num in range(pdf_reader.numPages):
           page = pdf_reader.getPage(page_num)
           text = page.extractText()

           translated_text = translator.translate(text, src=src_lang, dest=dest_lang).text

           c.drawString(100, 750, translated_text)
           c.showPage()

       c.save()

   if __name__ == "__main__":
       input_path = 'input.pdf'
       output_path = 'output.pdf'
       translate_pdf(input_path, output_path)