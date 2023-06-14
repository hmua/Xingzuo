*只是记录生成时间，以便之后总结经验*

从\
`{{'{'}}{site.categories|join:','}}`{:.liquid}\
改到
`{{'{'}}{site.categories|map:'name'|join:','}}`{:.liquid}
，
时间从1m40s缩减到50s。
