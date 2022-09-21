{%assign a=site.posts|where:"title",include.title|first%}
>#### {{a.title}}
>{{a.excerpt}}
