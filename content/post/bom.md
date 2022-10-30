---
date: "2022-10-30"
title: Unicode BOM and Excel
type: post
---
If you have tried generating CSV files that include non-ascii characters you will have noticed that these show up as weird and double letters such as Ã¥ Ã¤, and Ã¶ for the Swedish letters Å, Ä, and Ö respectively.

When this happens in web pages there is a mismatch between the declared and actual encoding of the page. This could for example happen if you create a page encoded in Unicode but not sent as such. The above example would have been easily solved by including a simple `Content-Type: text/html; charset=utf-8` header in the response to instruct the browser how to interpret the file if that was the case.

When it comes to local files there are no such headers though so the software on your computer has to make an educated guess based on the file name and contents. Excel does this when opening a CSV file by looking for a [byte order mark (BOM)](https://en.wikipedia.org/wiki/Byte_order_mark) which is unique to Unicode. When it cannot find this it defaults to some other encoding.

Making sure to include a default BOM in any output when generating a CSV file guarantees that the content is read as intendend. Given that the actual input is Unicode of course, but that is almost always the case.

For PHP this is as simple as adding an `fwrite` before any calls to `fputcsv`.
```php
fwrite($f, "\xEF\xBB\xBF");
fputcsv($f, $headers);
// etc.
```

Python has a different approach in that encoding can be specified for the outputed file and Python will handle these things automatically.
```python
with open(file, "w", encoding="utf-8-sig") as f:
    csv.writer(f).writerow(headers)
    # etc.
```
