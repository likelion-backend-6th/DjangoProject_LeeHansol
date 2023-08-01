# DjangoProject_LeeHansol

def post_list(request, tag_slug=None):
    page_number = request.GET.get('page', 1)
    page_list_query = Post.objects.filter(status=Post.Status.PUBLISHED)
    if tag_slug:
        tag = get_object_or_404(Tag, slug=tag_slug)
        page_list_query = page_list_query.filter(tags__in=[tag])

    paginator = Paginator(page_list_query, per_page=3)
    try:
        posts = paginator.page(page_number)
    except PageNotAnInteger:
        posts = paginator.page(1)
    except EmptyPage:
        posts = paginator.page(paginator.num_pages)
    return render(request, 'blog/post/list.html', {'posts': posts})

    
    이런 코드가 있을 때 맨 아래줄의 {'posts': posts} 이런 형식의 코드들이 무엇을 의미하는 지 궁금합니다.
