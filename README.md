# get-parameter
JavaScriptでURLのパラメーターを取得する

## 説明
URLパラメーター部分の文字列は"document.location.search"プロパティで取得できます。  
substring(1)メソッドを呼び出すことで2文字目以降の文字列を取り出します。(URLパラメーターが"?q=ABCD&m=30"であれば"q=ABCD&m=30"を取得します。)  

続いて、取得した文字列をsplit('&')により'&'区切りで分割をします。  
取得した文字列が"q=ABCD&m=30"であれば、parameters[0]にq=ABCD、parameters[1]にm=30が割り当てられます。  

さらにparametersの個々の要素について'='で区切りをし、値とパラメーター名を取得し、result連想配列に格納して戻り値として返します。

    function GetQueryString() {
    if (1 < document.location.search.length) {
      // 最初の1文字 (?記号) を除いた文字列を取得する
     var query = document.location.search.substring(1);

      // クエリの区切り記号 (&) で文字列を配列に分割する
     var parameters = query.split('&');

    var result = new Object();
    for (var i = 0; i < parameters.length; i++) {
      // パラメータ名とパラメータ値に分割する
     var element = parameters[i].split('=');

      var paramName = decodeURIComponent(element[0]);
      var paramValue = decodeURIComponent(element[1]);

      // パラメータ名をキーとして連想配列に追加する
       result[paramName] = decodeURIComponent(paramValue);
    }
    return result;
    }
    return null;
    }


## 実行結果
HTMLファイルを表示すると下図の表示結果となります。
<img src="https://github.com/nak-244/get-parameter/blob/master/img/none.png">

URLの末尾にパラメーター"q"を追加します。(URLの末尾に?q=北海道を追加しました。）
<img src="https://github.com/nak-244/get-parameter/blob/master/img/hokkaido.png">
