import requests as r
import lxml.html as lh
import pandas as pd
page = r.get("http://www.nepalstock.com/indices")
page
page.status_code ### we did this in order to check whether the page downloaded succesfully or not
### for the page content
page.content
doc = lh.fromstring(page.content)
#### parsing data in table
tr_elements = doc.xpath('//tr')
### checking the length of TR elements 
[len(T) for T in tr_elements[:12]]
# for header names
col = []
i=0
for t in tr_elements[1]:
    i+=1
    name = t.text_content()
    print ('%d"%s"'%(i,name))
    col.append((name,[]))
    for j in range(2,len(tr_elements)):
    ###T is our j'th row
    T=tr_elements[j]
    
    ###If row is not of size 5, the //tr data is not from our table 
    if len(T)!=5:
        break
    
    ###i is the index of our column
    i=0
    
    ###Iterate through each element of the row
    for t in T.iterchildren():
        data=t.text_content() 
        #Check if row is empty
        if i>0:
        ###Convert any numerical value to integers
            try:
                data=int(data)
            except:
                pass
        ###Append the data to the empty list of the i'th column
        col[i][1].append(data)
        #Increment i for the next column
        i+=1
[len(C) for (title,C) in col] ### this is to check the lenght of column whether or not they are the same
Dict = {title:column for (title,column) in col}
df = pd.DataFrame(Dict)
print(df)
