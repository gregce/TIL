# Reading / writing data using Zipfile 

Have you ever received a very large zipfile that you didn't want to decompress due to space/memory constraints?

Example Use Case:
You've received a very large zip file containing data that happens to be formatted incorrectly or when is decompressed results in a corrupted file and... you have to programatically address these issues

### Inspect to see the name of file within zip

```
import zipfile

zip = zipfile.ZipFile('your_zip_file.zip')
print zip.namelist()
```

### Once you know the name / names of the file you want to access
#### Let's say you want to add a , to each line (stopping after 100 lines) and write that that to a new file

```
import zipfile
import os

lines = 100

file = open('your_fixed_file.json', 'w')

zip = zipfile.ZipFile('/Users/gregce/Desktop/zendesk_tickets_comments_json.zip')

with zip.open('your_corrupted_file.json') as f:
    for i, l in enumerate(f):
        if i == lines:
            break
        file.write(l+',')
```
