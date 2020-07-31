装饰器学习：
def login_request(view_func):
    def inner(request, *args, **kwargs):
        uid = request.session.get('uid')
        if not uid:
            return redirect('/login')
        result = view_func(request, *args, **kwargs)
        return result
    return inner
