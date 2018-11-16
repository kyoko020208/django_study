# django_studyメモ
①DjangoはMTVモデルを採用している。
- M: model
- T: template
- V: view
https://www.sejuku.net/blog/wp-content/uploads/2018/03/django_mtv-640x426.png

②モデル参照（FireignKey)
#ForeignKeyで、Choiceがquestionを参照できる。
    on_deleteは、参照するオブジェクトが削除されたときに、それと紐づけられたオブジェクトも一緒に削除するのか、
    それともそのオブジェクトは残しておくのかを設定するもの
    CASCADEは削除するオブジェクトに紐づいたオブジェクトを全て削除。
    (以下サンプルコード)
    
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

③render関数：テンプレートを使った表示の仕方
render() 関数は、第1引数として request オブジェクトを、第2引数としてテンプレート名を、第3引数（任意）として辞書を受け取ります。
この関数はテンプレートを指定のコンテキストでレンダリングし、その HttpResponse オブジェクトを返します。
return render(request, 'polls/index.html', context)

④Path関数：
第一引数：route...ドメイン以下のURL
第二引数：view...ビュー関数、例：views.index
第三引数（オプション）kwargs：任意のキーワード引数を辞書として対象のビューに渡せます。
第四引数（オプション）name：urlに名前をつけておく

⑤include関数：他の URLconf への参照することができます。

⑥model.objects: おまじない。データベースにアクセスする。

⑦templateの書き方ーその一
action(どこに送るか)、method(どうやって送るかを指定)
<form action="{% url 'polls:vote' question.id %}" method="post">
    
⑧templateの書き方ーその二
{% csrf_token %}はおまじない（脆弱性対策）

⑦templateの書き方
