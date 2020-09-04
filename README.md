分页类：
class CustomPaginator(Paginator):
    def __init__(self,current_page, per_pager_num,*args,**kwargs):
        # 当前页
        self.current_page = int(current_page)
        # 最多显示的页码数量 11
        self.per_pager_num = int(per_pager_num)
        super(CustomPaginator,self).__init__(*args,**kwargs)
    def pager_num_range(self):
        # 当前页
        #self.current_page
        # 最多显示的页码数量 11
        #self.per_pager_num
        # 总页数
        # self.num_pages
        if self.num_pages < self.per_pager_num:
            return range(1,self.num_pages+1)
        # 总页数特别多 5
        part = int(self.per_pager_num/2)
        if self.current_page <= part:
            return range(1,self.per_pager_num+1)
        if (self.current_page + part) > self.num_pages:
            return range(self.num_pages-self.per_pager_num+1,self.num_pages+1)
        return range(self.current_page-part,self.current_page+part+1)

视图函数：
r1_list = r1_result.objects.all()
current_page = request.GET.get('p', 1)
paginator = CustomPaginator(current_page, 6, r1_list, 3)
posts = paginator.page(current_page)

page.html:
{% include 'parger.html' %}

parger.html:
{% if posts.has_previous %}
    <a href="page?p={{ posts.previous_page_number }}">上一页</a>
{% endif  %}
{% for i in posts.paginator.pager_num_range %}
    {% if i == posts.number %}
        <a href="page?p={{ i }}" style="font-size: 30px"> {{ i }}</a>
        {% else %}
        <a href="page?p={{ i }}">{{ i }}</a>
    {% endif %}
{% endfor %}
{% if posts.has_next %}
<a href="page?p={{ posts.next_page_number}}">下一页</a>
{% endif %}
<span> {{ posts.number }}</span>
<span>/ {{ posts.paginator.num_pages }}</span>
