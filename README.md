### Imgur
---
https://imgur.com/

https://github.com/Imgur

---
### Online WebStorage directory オンライン ストレージ　（サンプル用）
Instead of your own directory - ./img/background.jpg, uploading that images and then set down this url - https://imgur.com/lVtazJc

Account1 Repository img-Storages
#### tkgcci linked fb
https://imgur.com/lVtazJc

Account2
...

```

```

```
```

```rb
# api uploader
# imgur.rb
# ClientID, Client Secret 

require 'httpclient'

class Imgur

  URL = 'https://api.imgur.com/3/image'
  
  def initialize(client_id)
    @client_id = client_id
  end
  
  def anonymous_upload(file_path)
    auth_header = { 'Authorization' => 'Client-ID' + @client_id }
    upload(auth_header, file_path)
  end
  
  private
  
  def upload(auth_header, file_path)
    http_client = HTTPClient.new
    File.open(file_path) do |file|
      body = { 'image' => file }
      @res = http_client.post(URI.parse(URL), body, auth_header)
    end
    
    result_hash = JSON.load(@res.body)
    p result_hash
    result_hash['data']['link']
  end
  
end

# anonymouse_upload.rb
require './imgur.rb'
require 'json'

if ARGV.length < 2
  puts "usage"
  puts "ruby anonymous_upload [client_id] [image file path]"
  exit
end

p Imgur.new(ARGV[0]).anonymous_uplaod(ARGV[1])



```
