# django_studyメモ
①DjangoはMTVモデルを採用している。
- M: model
- T: template
- V: view
https://www.sejuku.net/blog/wp-content/uploads/2018/03/django_mtv-640x426.png

②モデル参照
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    #ForeignKeyで、Choiceがquestionを参照できる。
    on_deleteは、参照するオブジェクトが削除されたときに、それと紐づけられたオブジェクトも一緒に削除するのか、
    それともそのオブジェクトは残しておくのかを設定するもの。
    CASCADEは削除するオブジェクトに紐づいたオブジェクトを全て削除。
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
