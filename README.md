# httpd_contents_image

# コンテンツを含むイメージの作成
- コンテナを起動する
-- docker run -dit --name webcontent -p 8080:80 httpd:2.4
- index.htmlの作成
-- $workディレクトリにindex.htmlを作成する。(/home/xxxx/work_docker/httpd_contents_image/) 
- コンテナの中にindex.htmlをコピーする
-- docker cp /home/xxxx/work_docker/httpd_contents_image/index.html webcontent:/usr/local/apache2/htdocs
- mycustomed_httpdという名前のイメージを作成する
-- docker commit webcontent mycustomed_httpd
- 作成したイメージを確認する
-- docker image ls
- 作成したイメージを使用する
-- docker run -dit --name webcontent_new -p 8081:80 mycustomed_httpd
- 作成したイメージがコンテナで動いているか確認する
-- docker ps
- 動作確認
-- docker exec -it webcontent_new /bin/bash
-- cat /usr/local/apache2/htdocs/index.html
-- http://localhost:8081
- 後始末
-- docker stop webcontent webcontent_new
-- docker rm webcontent webcontent_new
-- docker image rm mycustomed_httpd
