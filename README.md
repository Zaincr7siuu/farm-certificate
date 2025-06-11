# farm-certificate
# Re-import necessary libraries after environment reset
import fitz  # PyMuPDF

# Re-define file path since previous session was reset
pdf_path = "/mnt/data/��سجل ريان العثمان � (2).pdf"

# Load the original PDF
doc = fitz.open(pdf_path)

# Define the old and new owner name
old_name = "خالد الفرحان"
new_name = "عبد العزيز عيسى صالح الطريفي"

# Search and replace the owner's name on all pages
for page in doc:
    text_instances = page.search_for(old_name)
    for inst in text_instances:
        page.add_redact_annot(inst, fill=(1, 1, 1))  # White out the old name
    page.apply_redactions()
    for inst in text_instances:
        page.insert_text(inst.tl, new_name, fontsize=12, fontname="Arial", color=(0, 0, 0))

# Save the modified PDF
output_path = "/mnt/data/Updated_Certificate.pdf"
doc.save(output_path)
doc.close()

output_path
