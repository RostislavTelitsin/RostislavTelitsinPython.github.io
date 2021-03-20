# Rostislav Telitsin Python Portfolio
python portfolio

All my projects in python are developed for internal using only and related to my current job. That's why I cannot publish them. But I can breafly describe the methods I used

## OS and files

Sometime I need to work with some files, uzip them and rename
- For example this part of code check if 'sample.xlsx' is exist and detele it. It alsomakes the list of excel files:
~~~
    if os.path.isfile('sample.xlsx'):
        os.remove('sample.xlsx')

    files = os.listdir()
    '''maiking the list of excel files'''
    file_list = []
    for file in files:
        if file[-4:] == 'xlsx':
            file_list.append(file)
~~~

- This part of code unzip all zip files in folder and rename it:
~~~
for file in DIRname:
    if file.split(".")[1] == "zip":

        if len(file.split("_"))==4:
            NeName = file.split("_")[2] + "_" + file.split("_")[3]
        else:
            NeName = file.split("_")[2]
        
        NeName = NeName.split(".")[0]
        print(file, "\n")
        zp = ZipFile(file, 'r')
        zp.extractall()
        os.rename(file[:-4] + '.txt', 'CFGMML-' + NeName + '-erunda.txt')
~~~        

- This part of code works with excel file using **openpyxl** lib:
~~~ 
i=0
    for file_name in file_list:
    #    print(file_name)
        wb = load_workbook(file_name)
        sheet = wb.active
        for NE_num in range(2, sheet.max_row + 1):
            if sheet.cell(row=NE_num, column=1).value:
                print(sheet.cell(row=NE_num, column=1).value)
                ws_com.cell(row=2 + i, column=1).value = file_name[:-5]
                ws_com.cell(row=2 + i, column=2).value = sheet.cell(row=NE_num, column=1).value
                ws_com.cell(row=2 + i, column=3).value = sheet.cell(row=NE_num, column=2).value
                ...
                ws_com.cell(row=2 + i, column=12).value = sheet.cell(row=NE_num, column=11).value
                if sheet.cell(row=NE_num, column=11).value:
                    xxx = str(sheet.cell(row=NE_num, column=11).value)
                    yyy = ent_id_ver(xxx)
                    print(yyy)
                    ws_com.cell(row=2 + i, column=13).value = yyy[0]
                    ws_com.cell(row=2 + i, column=14).value = yyy[1]
                i += 1
    wb_com.save("sample.xlsx")
~~~ 

## Binance
I also have some expirience with Binance criptocurrency working. I used **requests** lib interoperability with binance server, binance **API** to get data from server and **keras** lib to predict market trend

- this part of code requests data from server using Binance API:
~~~ 
    def collect_data(self, startTime, endTime):
        url = 'https://api.binance.com/api/v3/klines'
        limit = '1000'

        req_params = {
            'symbol': self.name,
            'interval': self.interval,
            'startTime': startTime,

            'endTime': endTime,
            'limit': limit
        }
        data = requests.get(url, params=req_params)
        data = np.asarray(json.loads(data.text))
        return data
~~~ 
