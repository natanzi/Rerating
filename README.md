# Rerating the international Call Details Record (CDR) for Telecom industry
Longest matching for international numbers...
The below-attached python can be used in Monitoring and rerating of telecom CDRx of all revenue streams.
This means that you can match each B number with originating of its country's destination to charge them.

[Longest matching.txt](https://github.com/natanzi/Rerating/files/7127803/Longest.matching.txt)
# 
import cx_Oracle
import csv
import smtplib, ssl

ipaddress = 'IP'
username = 'YOU DB USER'
password = 'YOUR PASSWORD USER'
port = '***'
tnsname = '***'

from datetime import date, timedelta
today = date.today()
yesterday = today - timedelta(days = 1)
x = today.strftime("%Y%m%d")
y = yesterday.strftime("%Y%m%d")

try:

    dsn = cx_Oracle.makedsn(ipaddress, ***, service_name="***")
    db = cx_Oracle.connect("YOU DB USER", 'YOUR PASSWORD USER', dsn, encoding="UTF-8")
except Exception as e:
    content = (tnsname + ' is Unreachable,The reason is ' + str(e)).strip()
    print(content)

cursor = db.cursor()
x = "'00%'"
dif = pd.read_excel("tmp\DB.XLSX")

r = cursor.execute('SELECT /*+ full(t) parallel(t,06)*/ Select *  partition for (%s) where rownum < 200  and B_NUMBER LIKE %s' %(y,x))
data = cursor.fetchall()

print("CREATING CELLCFG CSV")
