from tika import parser
import re
import os
import glob
import numpy as np

input_path = ('INDSÆT_PATH_MED_KONTOUDSKRIFTER_PDF_FORMAT')

samlet_pris = 0.0
over100_list = []
under100_list = []

for input_file in glob.glob(os.path.join(input_path, '*.pdf')):
    filename = os.path.basename(input_file)
    parsedPDF = parser.from_file(input_file)
    tekst = ''.join(parsedPDF['content'])
    Regex = re.compile(r'Vinstuen.*')
    mo = Regex.findall(tekst)

    Regex_pris_str = ''.join(mo)
    Regex_pris_under100 = re.compile(r'\d\d,00')
    Regex_pris_over100 = re.compile(r'\d\d\d,00')

    mo_pris_under100 = Regex_pris_under100.findall(Regex_pris_str)
    mo_pris_under100 = [pris.replace(',', '.') for pris in mo_pris_under100]
    under100_list.append(mo_pris_under100)
    under100_list = list(filter(None, under100_list))

    mo_pris_over100 = Regex_pris_over100.findall(Regex_pris_str)
    mo_pris_over100 = [pris.replace(',', '.') for pris in mo_pris_over100]
    over100_list.append(mo_pris_over100)
    over100_list = list(filter(None, over100_list))
    print(under100_list)



for item in over100_list:
    samlet_pris += sum([float(e) for e in item])

for item in under100_list:
    samlet_pris += sum([float(e) for e in item])

print('\n' + 'Du har cirka brugt: ' + str(samlet_pris) + 'kr på Vinstuen')

       
       


    
    
    
    
