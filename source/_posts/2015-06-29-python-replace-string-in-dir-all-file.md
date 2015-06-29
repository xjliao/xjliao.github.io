title: python 替换指定文件夹内所有文件的指定内容
date: 2015-06-29 15:10:05
categories:
- Python
tags:
- Python

---

code

{% codeblock lang:python a.py %}
import os
import os.path

old_str = "old_str"
new_str = "new_str"

inws = "/Users/xjliao/Desktop/tmep"

def is_md(f):
    hz_list = ['.md']
    test_str = f.lower()
    for hz in hz_list:
        if test_str.endswith(hz):
            return(True)

    return(False)

def main():
    for wroot, wdirs, wfiles in os.walk(inws):
        for wfile in wfiles:
            infile = os.path.join(wroot, wfile)
            if is_md(infile) == False:
                continue

            cnts=file(infile).read()
            if old_str in cnts:
                outfile = infile
                fo = open(outfile, 'w')
                cnts_new = cnts.replace(old_str, new_str)
                fo.write(cnts_new)
                fo.close()
                print(wfile)
            else:
                pass

if __name__ == '__main__':
        main()
{% endcodeblock %}