---
title: tmail
id: 26
categories:
  - 未分類
date: 2013-07-03 16:56:43
tags:
---

[ruby]
def mail_data(mFile)
  file = File.open(mFile).read
  mail = TMail::Mail.parse(file)
  #p mail.to # 送信先
  #p mail.from # 送信元
  idx = 1 # ファイル名
  mail.parts.each do |m|
    if nil != m['content-disposition']
      m.base64_decode
      attach_fileNm = m['content-disposition']['filename']
      #File.open(&quot;#{CLIENTDATAPATH}/#{attach_fileNm}.#{ext(m)}&quot;, 'w') do |f|
      File.open(&quot;#{CLIENTDATAPATH}/#{attach_fileNm}&quot;, 'w') do |f|
        f.write m.body
      end
    end
    idx += 1
  end
end

CTYPE_TO_EXT = {
  'image/jpeg'               =&gt; 'jpg',
  'image/gif'                =&gt; 'gif',
  'image/png'                =&gt; 'png',
  'image/tiff'               =&gt; 'tiff',
  'text/plain'               =&gt; 'txt',
  'application/vnd.ms-excel' =&gt; 'csv'
}

def ext( mail )
  CTYPE_TO_EXT[mail.content_type] || 'txt'
end
[/ruby]

http://ecpplus.net/weblog/ruby%E3%81%A7%E5%8F%97%E4%BF%A1%E3%83%A1%E3%83%BC%E3%83%AB%E8%A7%A3%E6%9E%90/