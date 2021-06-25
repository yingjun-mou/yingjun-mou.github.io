---
title: 'Tabular data extraction'
date: 2021-06-03
permalink: /posts/2021/06/Tabular data extration/
tags:
  - Tabular data
  - Conda
categories:
  - Coding
  - Tutorial
  - Research
---


Tabular data extraction
======

[presentation link](https://www.youtube.com/watch?v=Irf6kdl0lAA&list=LL&index=3) 

## 1. Tabula
**Limitations**
1. Will break multi-line cells into multi lines, many of them may be empty

## 2. pdftotext
**Usage**
- `pdftotext foo.pdf -layout -`\
**Limitations**
1. Output is as text file, need to further extract 
2. Lose the structural info
3. Time consuming

## 3. Camelot

[camelot documentation link](https://camelot-py.readthedocs.io/en/master/) 

**Dependencies**
```
# pip install camelot-py[cv]
# or
# conda install -c conda-forge camelot-py
# warning: not camelot, but camelot-py[cv], otherwise read_pdf will not be found
```

**(Huge) Limitation**
1. Camelot only works with text-based PDFs and not scanned documents. To verify, open pdf in Adobe Reader and try to select text using cursor.

**Advantages**
1. Flag sup/subscript to avoid error. `tables = camelot.read_pdf('foo.pdf', flag_size=True)`
2. Strip unnecessary character. `tables = camelot.read_pdf('foo.pdf', strip_text=' .\n')`
3. shift text in cells that span multiple rows/columns. `Shift_text=['l', 't']`
4. Copy and populate text in cells that span multiple rows/columns. `copy_text=['l', 't']`
5. Export the tables to different formarts. 
```python
tables.export('foo.csv', f='csv', compress=True)
tables[0].to_csv('foo.csv') # to_json(), to_excel() to_html() or to_sqlite()
```
6. Analyze result: `print(tables[0].parsing_report)`
7. Specify pages: `camelot.read_pdf(file, pages='1,4-10,20-end', flavor = 'lattice')` 

8. After we get the table from pdf, we can convert to dataframe using `table.df` or to lists using `table.data`

9. The tabular extraction from pdf sometimes will capture the plot(because they also have grid). To solve this, we can simply replace '' in dataframe with NaN, and use:\
```python
df = df.replace('', np.nan)  
if not df.isna().values.all():
    # do something with those df we really want
```

10. The camelot will add `\n` into the text of a multi-row cell. In order to solve it, add an arg `strip_text=' .\n'` for `camelot.read_pdf()`.

11. PSSyntax error dealing with pdfs with Chinese characters.
It will log something like `raise PSSyntaxError(error_msg) pdfminer.psparser.PSSyntaxError: Invalid dictionary construct: [/'Type', /'Font', /'Subtype', /'Type0', /'BaseFont', /b"b'", /"ABCDEE+\\xcb\\xce\\xcc\\xe5'", /'Encoding', /'Identity-H', /'DescendantFonts', <PDFObjRef:17>, /'ToUnicode', <PDFObjRef:23>]`.
To fix it, the github recommend using command line to fix the pdf files. And that's what I did. 
```python
for pdf_filename in pdf_list:
    temp_name = pdf_filename.replace('.pdf', '_temp.pdf')
    fix_pdf_command = 'gs -o ' + temp_name + ' -sDEVICE=pdfwrite -dPDFSETTINGS=/prepress -dQUIET ' + pdf_filename  # new name then old name
    os.system(fix_pdf_command)
    os.replace(temp_name, pdf_filename)
```
But some other people also suggested fixing by [modifying the source codes](https://www.cnblogs.com/Eeyhan/archive/2019/12/30/12111371.html).



## 4. CSV table view in Pycharm
To better visualize csv file as table in pycharm:
1. Professional version
2. Have to add break point by typing `# %%` or clicking the line after my df variable
3. Open the panel for "show variable"
4. Right click the df variable and show as dataframe


## 5. Semantic Scholar (S2) API
How to use SciRex data to access the source paper?\
Use Semantic Scholar (S2) API to search paper using doc_id in SciRex dataset. [Documentation link](https://api.semanticscholar.org/)
- Use direct url: https://api.semanticscholar.org/doc_id
There are some alternatives:
1. Use DOI : https://api.semanticscholar.org/10.1038/nrn3241
2. ArXiv ID : https://api.semanticscholar.org/arXiv:1705.10311
3. Corpus ID : https://api.semanticscholar.org/CorpusID:37220927

However, these options above are for manual inspection. You clicked them, you land on specific webpages. In order to let machine to automatically crawl detail info about the papers, we need to write a bit codes. [Documentation link](https://pypi.org/project/semanticscholar/)

```
pip install semanticscholar

>>> import semanticscholar as sch
>>> paper = sch.paper('10.1093/mind/lix.236.433', timeout=2)
>>> paper.keys()
dict_keys(['abstract', 'arxivId', 'authors', 'citationVelocity', 'citations', 'doi',
'influentialCitationCount', 'paperId', 'references', 'title', 'topics', 'url', 'venue', 'year'])
>>> paper['title']
'Computing Machinery and Intelligence'
>>> for author in paper['authors']:
...     print(author['name'])
...     print(author['authorId'])

```

Notes: seems that semanticscholar, like many other pachages, are avaialble on pip, but not available on conda. I found a workaround: 
1. with the conda environment activated, `conda install pip`. Then `pip install xx`. 
2. Another way to solve it is to open the **Anaconda prompt**, and type `pip install xx` there. It will install the package for all conda virtual envs.

## 6. Arxiv API
[Documentation link](https://pypi.org/project/arxiv/)\
Download pdf/source given a arxiv id.

## 7. Retrieve the LaTex file of paper
How to get the LaTex file given the archive file?\
There are 4 different kinds of archive files: (1).zip (2).rar (3).gz (4).tar. Although the arxiv website instruct me to manually add an .gz extention, I found that adding .tar extention is better (if I use .gz, the python codes of unzipping will yiled a binary file with the same name, instead of yileding those actual compressed files).

1. Unzip an archive file
- Dependency: `pip install patool`. Import: `import patoolib`.
- To extract: `patoolib.extract_archive(target_filename, outdir='unpack')`
- How to filter the files with `.tex`?\
```
import glob
path = "unpack/*.tex"
filename = glob.glob(path)[0]
```
The path is a list which may contains more than one instances.

2. Understand the Latex file structure:
There are multiple types of environment enclosed by `\begin{environment_type}` and `\end{environment_type}`.
	1. document
	2. abstract
	3. IEEEkeywords
	4. figures* (include `\subfloat` column and `\caption` below each of them)
	5. itemize (a list of bullet points, with `\item` for each)
	6. equation
	7. align (similar to equation, but format slitly differently)
	8. array (can be used for showing matrix)
	9. **table** (include `\caption`, `\begin{tabular}`)
	10. **tabular**
		```latex
		\begin{tabular}{|l|cc|}
			\hline
			\multirow{2}{*}{Methods}  &mean IU &mean IU \\
	           &VOC2011 test  &VOC2012 test \\
	        \hline\hline
	        FCN-8s~\cite{long2015fully}  &62.7 &62.2 \\
	        DLDL-8s &64.9 &64.5 \\
	        DLDL-8s+CRF &\textbf{67.6} &\textbf{67.1} \\
	        \hline
		\end{tabular}
		```

3. Delete all the comments from a Latex file

Comments are started with `%` in tex file. I didn't realized how anoying they are until I have done most parts of the parsing.\

To achieve this, I tried **arxiv-latex-cleaner** [[Link od arxiv-latex-cleaner]](https://github.com/google-research/arxiv-latex-cleaner/), but got no luck. Eventually end up using file io.\
```python
# Clean up all the comments
with open(latex_filename, "r") as f:
    lines = f.readlines()
with open(latex_filename, "w") as f:
    for line in lines:
        if len(line.strip("\n")) and line.strip("\n")[0] != '%':
            f.write(line)
```

## 8. TexSoup: parse a Latex file

1. **TexSoup** is a package I found convenient to nevigate latex file. [Documentation link](https://texsoup.alvinwan.com/docs/quickstart.html)\
- Install: `pip install texsoup`.
- Import: `from TexSoup import TexSoup`
- Soupify a latex file:\
```python
with open("main.tex") as f:
	soup = TexSoup(f)
```
or pass the latex string: `soup = TexSoup(latex_str)`

2. Data structure of a soup:\
There are only 3 different types of python objects: (1)**command**, (2)**Text**, (3)**Environment**.

3. Filter out a specific types of enviornment\
`soup.find_all('table')`, if there are more than one types, pass into a list such as `soup.find_all(['table','table*'])`

4. Strip all the uncessary tokens and access the content: `.contents`, e.g. `soup.find_all('table')[i].contents`. However, I found `.text` works cleaner. The find_all will return a list of **TextNode** objects. **TextNode** instance has attribute `.text`.

5. Delete the **citation** and **unecessasry superscript** and **hline** info before converting TextNode to text?
```python
if node.name == 'tabular':
    for subnode in node:
        if hasattr(subnode, 'name') and (subnode.name == 'hline' or subnode.name == 'cite' or subnode.name == 'rlap'):
            subnode.delete()
```


6. The `.text` method will omit the speicial charater `\pm`(plus-minus sign). `print(u"\u00B1")` in python.

7. Try `TexSoup.TexSoup(tex_code, skip_envs=(), tolerance=0)`, https://texsoup.alvinwan.com/docs/main.html

8. If we want to access the structural info such as 'c c', use `soup.tabular.args[0].string`

9. Clean the LaTex string
- White spaces: `s = s.strip()`
- Not only white spaces, but tab, new line: `s = s.strip(' \t\n\r')`
- Not only remove left and right, but also all white spaces in between: \
```python
import re
print(re.sub('[\s+]', '', s))
```

10. Find the caption of each tabular instance
```python
for node in soups:
	if node.name == 'table':
	    for subnode in node:
		    if subnode.name == 'caption':
	            	caption = subnode.text		            
```

11. Convert Latex math expressions to python
Use **unicodeit** `pip install unicodeit`\
```python
import unicodeit
print(unicodeit.replace('\\alpha'))

```
But if we directly unicode everything in dataframe, there may be a chance that it will be coincidentally identical to some other unrecognized strings. For example, a unicoded '250\%' will be displayed as a shaded block '▒'.\
To solve it, for each string, I find the occurences of slash, then find the 1st numeric char after it. We will only unicode the substring in between:\
```python
def clean_tex(inp):
    inp = inp.strip(' \t\n\r').strip('~').replace('~', ' ')
    # locate each slash and the 1st numeric char after this slash
    # in between them will need to be unicoded
    target_str = inp
    while target_str.find('\\') != -1:
        first_slash_pos = target_str.find('\\')
        first_num_pos = re.search(r"\d", target_str[first_slash_pos:]) # first numeric char
        if not first_num_pos:
            target_str = target_str[:first_slash_pos] + unicodeit.replace(target_str[first_slash_pos:])
        else:
            target_str = target_str[:first_slash_pos] + unicodeit.replace(target_str[first_slash_pos:first_num_pos.start()]) \
                         + target_str[first_num_pos.start():]

    return target_str
```

Problems of unicodes:\
Seems that unicode has issueus dealing with subscript. e.g. `p_{emp}` works while `p_{gen}` doesn't. Some char were not recognized by unicodeit.\
To solve it, I have to change it to **latexcodec** and **pylatexenc**.\


12. How to modify the text of a node?
Seems that there is no available function to modify in place. The only workaround I found is to construct a new node with specific text, then replace the original node with the new one.

13. How to construct a new node with specific text, and specific name?
```python
new_textnode = TexNode(TexSoup.data.TexText("NEW TEXT"))
new_textnode = TexSoup.data.TexText("NEW TEXT")

new_textnode.name = 'NEW NAME'
subnode.replace_with(new_textnode)
```
14. Find the tabular node?
Warning:
- it can be 'tabular', or 'tabularx' or 'tabulary'.
- there may be more than one tabular node in one table node

15. Math related issue resulting exception during the Latex parsing.
Seems that TexSoup(at the point I installed it) is very error-prone when dealing with math env `$ X $` when formula gets complicated. Most of the time it is becuase TexSoup will recognize `$` together the the adjacent char before or after it. There are a few discussion on the Github, but I realized that the codes on master repo are different from the codes I pip installed a few days ago. Seems that they haven't released the updates on PyPI. And after I download the codes from master and manually replaced the source codes, the problem was solved.

Another reminder: after replacing the source codes in the library, needs to restart the python terminal to see the updates.


## 8. Other Python related issues

1. How to deal with multicolumn and multirow cells?
Convert dataframe to dictionary, iterate through each cell, if `cell==''`, replace it with the value on the top or left.\
In my case, I can easily deal with multicolumn by concatenate multiple repeating strings at the TexSoup node level. But couldn't deal with multirow cell in a similar way. So, when processing the dataframe, I can only deal with multirow.
```python
# replace empty cell with value above
df_dict = df.to_dict()
    num_col = len(df_dict)
    num_row = len(df_dict[0])
    for i in range(num_col):
        for j in range(num_row):
            if df_dict[i][j] == '' and j>0:
                df_dict[i][j] = df_dict[i][j-1]
``` 

2. How to open csv file with UTF-8 unicode?
`Data`---`From Text`---Set UTF-8 Unicode---Set delimiter to **comma**.

3.

4. How to use os to to create directory, delete, and filter files?
```
for filename in os.listdir(path):
    print(filename)
    if filename not in file_name:
        os.remove(filename)
```
or 
```python
for filename in glob.glob("mypath/version*"):
# can be glob.glob('/tmp', '*[0-9]*.jpg')
```

5. Fast convert a string to be valid for filename(alphanumeric)?
Fast way: \
```python
"".join(x for x in NAME if x.isalnum())
```
Better format with underscore: \
```python
for x in caption:
    if not x.isalnum():
        caption.replace(x, '_')
```


