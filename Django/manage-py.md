Model : 
```
class Question(models.Model):
    has_voted = models.ManyToManyField(User, through="Upvote", related_name="has_voted")

class Upvote(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    user = models.ForeignKey(User, on_delete=models.CASCADE, null=True, blank=True)
```
View :
```
def append_question(request):
    recent_questions = Question.objects.filter(date__gt=datetime.now() - timedelta(hours=1))
```
I want to order recent_questions by their count() of has_voted. How would I do this?
```
Question.objects.filter(date__gt=datetime.now() - timedelta(hours=1))\
        .annotate(num_votes=Count('has_voted'))\
        .order_by('-num_votes')
