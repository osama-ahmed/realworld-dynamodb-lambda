```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-5umpv4@email.com",
    "username": "author-5umpv4",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-5umpv4@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci01dW1wdjQiLCJpYXQiOjE1ODI1ODQ3MDIsImV4cCI6MTU4Mjc1NzUwMn0.ZG5TJgYI0aMSjfIjQO2V9_OU5eY7vEr6CY5vcG5ULOQ",
    "username": "author-5umpv4",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-yqxmmn@email.com",
    "username": "authoress-yqxmmn",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-yqxmmn@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy15cXhtbW4iLCJpYXQiOjE1ODI1ODQ3MDIsImV4cCI6MTU4Mjc1NzUwMn0.VWZ-OJbI_xYGci8AjhJ7d1lMC1LYgvBx04a48VR82fg",
    "username": "authoress-yqxmmn",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-5kyrjv@email.com",
    "username": "non-author-5kyrjv",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-5kyrjv@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItNWt5cmp2IiwiaWF0IjoxNTgyNTg0NzAyLCJleHAiOjE1ODI3NTc1MDJ9.14P0qJup_6xdS_mPnTP23DEtkpwOydlaQw5fn3Ilt3M",
    "username": "non-author-5kyrjv",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nhq88",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584702519,
    "updatedAt": 1582584702519,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-20ofa2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584702585,
    "updatedAt": 1582584702585,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-nhq88
```
```
200 OK

{
  "article": {
    "createdAt": 1582584702519,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-nhq88",
    "updatedAt": 1582584702519,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-20ofa2
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1582584702585,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-20ofa2",
    "updatedAt": 1582584702585,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/fa20bi
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [fa20bi]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-20ofa2

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1582584702585,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-20ofa2",
    "updatedAt": 1582584702585,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-20ofa2

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1582584702585,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-20ofa2",
    "updatedAt": 1582584702585,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-20ofa2

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1582584702585,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-20ofa2",
    "updatedAt": 1582584702585,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-20ofa2

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-20ofa2

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-20ofa2

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-20ofa2

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-20ofa2]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-20ofa2

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-5umpv4]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-nhq88/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1582584702519,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-nhq88",
    "updatedAt": 1582584702519,
    "favoritedBy": [
      "non-author-5kyrjv"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-nhq88
```
```
200 OK

{
  "article": {
    "createdAt": 1582584702519,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-nhq88",
    "updatedAt": 1582584702519,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-nhq88/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-nhq88_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-nhq88_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-nhq88/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1582584702519,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-nhq88",
    "updatedAt": 1582584702519,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-nhq88
```
```
200 OK

{}
```
```
GET /articles/title-nhq88
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-nhq88]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-20ofa2
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-5umpv4]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7gfs2s",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sjtfjf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703522,
    "updatedAt": 1582584703522,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7gfs2s",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "t3jzd5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-x7ut2s",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703564,
    "updatedAt": 1582584703564,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "t3jzd5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5zs3kq",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gd0gb3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703591,
    "updatedAt": 1582584703591,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5zs3kq",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "oobh50",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-m7k0zu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703618,
    "updatedAt": 1582584703618,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "oobh50",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ih4hmx",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-424bgq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703643,
    "updatedAt": 1582584703643,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ih4hmx",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3p9x1z",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mujcck",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703673,
    "updatedAt": 1582584703673,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3p9x1z",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tbo25o",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6b9yrc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703698,
    "updatedAt": 1582584703698,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tbo25o",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jqnems",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-76h4w2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703719,
    "updatedAt": 1582584703719,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jqnems",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hoilfu",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-eoqv0e",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703745,
    "updatedAt": 1582584703745,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hoilfu",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8udlxz",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sljb9w",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703772,
    "updatedAt": 1582584703772,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8udlxz",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2e4qkc",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-h8yqok",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703802,
    "updatedAt": 1582584703802,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2e4qkc",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "riz1io",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ltq92z",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703835,
    "updatedAt": 1582584703835,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "riz1io",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "h6s5tm",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-hdfpym",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703859,
    "updatedAt": 1582584703859,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "h6s5tm",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bhbmy4",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ufia3u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703881,
    "updatedAt": 1582584703881,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bhbmy4",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lud4sf",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-o9v1wh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703902,
    "updatedAt": 1582584703902,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lud4sf",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2fmxo8",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jl7313",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703923,
    "updatedAt": 1582584703923,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2fmxo8",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "a767np",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uqh6d3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703947,
    "updatedAt": 1582584703947,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "a767np",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "whlq6w",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-vzyvr0",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584703974,
    "updatedAt": 1582584703974,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "whlq6w",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "byak62",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nkicqv",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584704001,
    "updatedAt": 1582584704001,
    "author": {
      "username": "authoress-yqxmmn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "byak62",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dw8o6g",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3fx2bf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584704048,
    "updatedAt": 1582584704048,
    "author": {
      "username": "author-5umpv4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dw8o6g",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "dw8o6g",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584704048,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3fx2bf",
      "updatedAt": 1582584704048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "byak62",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584704001,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nkicqv",
      "updatedAt": 1582584704001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "whlq6w"
      ],
      "createdAt": 1582584703974,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vzyvr0",
      "updatedAt": 1582584703974,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a767np",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703947,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uqh6d3",
      "updatedAt": 1582584703947,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2fmxo8",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703923,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jl7313",
      "updatedAt": 1582584703923,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bhbmy4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703881,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufia3u",
      "updatedAt": 1582584703881,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h6s5tm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703859,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hdfpym",
      "updatedAt": 1582584703859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "riz1io",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703835,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ltq92z",
      "updatedAt": 1582584703835,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2e4qkc",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703802,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h8yqok",
      "updatedAt": 1582584703802,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8udlxz",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703772,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sljb9w",
      "updatedAt": 1582584703772,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jqnems",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703719,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-76h4w2",
      "updatedAt": 1582584703719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "tbo25o"
      ],
      "createdAt": 1582584703698,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6b9yrc",
      "updatedAt": 1582584703698,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3p9x1z",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703673,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mujcck",
      "updatedAt": 1582584703673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ih4hmx",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703643,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-424bgq",
      "updatedAt": 1582584703643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oobh50",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703618,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m7k0zu",
      "updatedAt": 1582584703618,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t3jzd5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703564,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x7ut2s",
      "updatedAt": 1582584703564,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7gfs2s",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703522,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sjtfjf",
      "updatedAt": 1582584703522,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "jqnems",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703719,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-76h4w2",
      "updatedAt": 1582584703719,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "whlq6w"
      ],
      "createdAt": 1582584703974,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vzyvr0",
      "updatedAt": 1582584703974,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "riz1io",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703835,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ltq92z",
      "updatedAt": 1582584703835,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3p9x1z",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703673,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mujcck",
      "updatedAt": 1582584703673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-yqxmmn
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "byak62",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584704001,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nkicqv",
      "updatedAt": 1582584704001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a767np",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703947,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uqh6d3",
      "updatedAt": 1582584703947,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h6s5tm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703859,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hdfpym",
      "updatedAt": 1582584703859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2e4qkc",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703802,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h8yqok",
      "updatedAt": 1582584703802,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "tbo25o"
      ],
      "createdAt": 1582584703698,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6b9yrc",
      "updatedAt": 1582584703698,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ih4hmx",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703643,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-424bgq",
      "updatedAt": 1582584703643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7gfs2s",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703522,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sjtfjf",
      "updatedAt": 1582584703522,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-5kyrjv
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-5umpv4&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "dw8o6g",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584704048,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3fx2bf",
      "updatedAt": 1582584704048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "whlq6w"
      ],
      "createdAt": 1582584703974,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vzyvr0",
      "updatedAt": 1582584703974,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-5umpv4&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "2fmxo8",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703923,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jl7313",
      "updatedAt": 1582584703923,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bhbmy4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703881,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufia3u",
      "updatedAt": 1582584703881,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "dw8o6g",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584704048,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3fx2bf",
      "updatedAt": 1582584704048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "byak62",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584704001,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nkicqv",
      "updatedAt": 1582584704001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "whlq6w"
      ],
      "createdAt": 1582584703974,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vzyvr0",
      "updatedAt": 1582584703974,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a767np",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703947,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uqh6d3",
      "updatedAt": 1582584703947,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2fmxo8",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703923,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jl7313",
      "updatedAt": 1582584703923,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bhbmy4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703881,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufia3u",
      "updatedAt": 1582584703881,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h6s5tm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703859,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hdfpym",
      "updatedAt": 1582584703859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "riz1io",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703835,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ltq92z",
      "updatedAt": 1582584703835,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2e4qkc",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703802,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h8yqok",
      "updatedAt": 1582584703802,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8udlxz",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703772,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sljb9w",
      "updatedAt": 1582584703772,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jqnems",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703719,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-76h4w2",
      "updatedAt": 1582584703719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "tbo25o"
      ],
      "createdAt": 1582584703698,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6b9yrc",
      "updatedAt": 1582584703698,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3p9x1z",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703673,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mujcck",
      "updatedAt": 1582584703673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ih4hmx",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703643,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-424bgq",
      "updatedAt": 1582584703643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oobh50",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703618,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m7k0zu",
      "updatedAt": 1582584703618,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t3jzd5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703564,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x7ut2s",
      "updatedAt": 1582584703564,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7gfs2s",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703522,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sjtfjf",
      "updatedAt": 1582584703522,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-yqxmmn/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-yqxmmn",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "byak62",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584704001,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nkicqv",
      "updatedAt": 1582584704001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a767np",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703947,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uqh6d3",
      "updatedAt": 1582584703947,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h6s5tm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703859,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hdfpym",
      "updatedAt": 1582584703859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2e4qkc",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703802,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h8yqok",
      "updatedAt": 1582584703802,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "tbo25o"
      ],
      "createdAt": 1582584703698,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6b9yrc",
      "updatedAt": 1582584703698,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ih4hmx",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703643,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-424bgq",
      "updatedAt": 1582584703643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7gfs2s",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703522,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sjtfjf",
      "updatedAt": 1582584703522,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-5umpv4/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-5umpv4",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "dw8o6g",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584704048,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3fx2bf",
      "updatedAt": 1582584704048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "byak62",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584704001,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nkicqv",
      "updatedAt": 1582584704001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "whlq6w"
      ],
      "createdAt": 1582584703974,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vzyvr0",
      "updatedAt": 1582584703974,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a767np",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703947,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uqh6d3",
      "updatedAt": 1582584703947,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2fmxo8",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703923,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jl7313",
      "updatedAt": 1582584703923,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lud4sf",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703902,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o9v1wh",
      "updatedAt": 1582584703902,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bhbmy4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703881,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufia3u",
      "updatedAt": 1582584703881,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h6s5tm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703859,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hdfpym",
      "updatedAt": 1582584703859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "riz1io",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703835,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ltq92z",
      "updatedAt": 1582584703835,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2e4qkc",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703802,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h8yqok",
      "updatedAt": 1582584703802,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8udlxz",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703772,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sljb9w",
      "updatedAt": 1582584703772,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hoilfu",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703745,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eoqv0e",
      "updatedAt": 1582584703745,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jqnems",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703719,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-76h4w2",
      "updatedAt": 1582584703719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "tbo25o"
      ],
      "createdAt": 1582584703698,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6b9yrc",
      "updatedAt": 1582584703698,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3p9x1z",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703673,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mujcck",
      "updatedAt": 1582584703673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ih4hmx",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703643,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-424bgq",
      "updatedAt": 1582584703643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oobh50",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703618,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m7k0zu",
      "updatedAt": 1582584703618,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5zs3kq",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1582584703591,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gd0gb3",
      "updatedAt": 1582584703591,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t3jzd5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1582584703564,
      "author": {
        "username": "author-5umpv4",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x7ut2s",
      "updatedAt": 1582584703564,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7gfs2s",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1582584703522,
      "author": {
        "username": "authoress-yqxmmn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sjtfjf",
      "updatedAt": 1582584703522,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "ih4hmx",
    "tag_4",
    "tag_mod_2_0",
    "tag_mod_3_1",
    "jqnems",
    "tag_7",
    "tag_mod_2_1",
    "2e4qkc",
    "tag_10",
    "7gfs2s",
    "tag_0",
    "tag_mod_3_0",
    "lud4sf",
    "tag_14",
    "tag_mod_3_2",
    "tag_a",
    "tag_b",
    "tag_6",
    "tbo25o",
    "riz1io",
    "tag_11",
    "h6s5tm",
    "tag_12",
    "bhbmy4",
    "tag_13",
    "tag_17",
    "whlq6w",
    "hoilfu",
    "tag_8",
    "3p9x1z",
    "tag_5",
    "t3jzd5",
    "tag_1",
    "a767np",
    "tag_16",
    "byak62",
    "tag_18",
    "oobh50",
    "tag_3",
    "5zs3kq",
    "tag_2",
    "8udlxz",
    "tag_9",
    "2fmxo8",
    "tag_15",
    "dw8o6g",
    "tag_19"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-wzi0di@email.com",
    "username": "author-wzi0di",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-wzi0di@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci13emkwZGkiLCJpYXQiOjE1ODI1ODQ3MDUsImV4cCI6MTU4Mjc1NzUwNX0.Knas6ykgRyhMHnPhorFK0xcUvtryK-1RfzNj6xx9yCo",
    "username": "author-wzi0di",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-vye4n8@email.com",
    "username": "commenter-vye4n8",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-vye4n8@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci12eWU0bjgiLCJpYXQiOjE1ODI1ODQ3MDUsImV4cCI6MTU4Mjc1NzUwNX0.7IiZTjN7j2fAqE6NLeeJjbTjDk0BNFlJsiD2zmaaBBk",
    "username": "commenter-vye4n8",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-co08ft",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1582584705445,
    "updatedAt": 1582584705445,
    "author": {
      "username": "author-wzi0di",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment 26f3u0"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "169bccd9-a146-4a7a-9b43-852873c31fa8",
    "slug": "title-co08ft",
    "body": "test comment 26f3u0",
    "createdAt": 1582584705490,
    "updatedAt": 1582584705490,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment hgi10d"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7b662d80-b479-4ae6-95be-cc5743d4a33e",
    "slug": "title-co08ft",
    "body": "test comment hgi10d",
    "createdAt": 1582584705522,
    "updatedAt": 1582584705522,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment oaieo8"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "a96e20f6-ec32-45fb-b533-50f3f52f7f3e",
    "slug": "title-co08ft",
    "body": "test comment oaieo8",
    "createdAt": 1582584705559,
    "updatedAt": 1582584705559,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment twjjte"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "533e1670-3d92-44f5-9e70-a331aae975df",
    "slug": "title-co08ft",
    "body": "test comment twjjte",
    "createdAt": 1582584705593,
    "updatedAt": 1582584705593,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment x9jhso"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e10b7fa0-8d66-45f5-87ed-b81510e9f848",
    "slug": "title-co08ft",
    "body": "test comment x9jhso",
    "createdAt": 1582584705623,
    "updatedAt": 1582584705623,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment y72p20"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fbe7e984-6107-4e6a-a6f3-8a813fc695eb",
    "slug": "title-co08ft",
    "body": "test comment y72p20",
    "createdAt": 1582584705652,
    "updatedAt": 1582584705652,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment 71sv83"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d35fab95-d2c5-4278-85c2-e104d87283eb",
    "slug": "title-co08ft",
    "body": "test comment 71sv83",
    "createdAt": 1582584705685,
    "updatedAt": 1582584705685,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment uaiugs"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "92a6aa29-2f56-431c-b83e-47923a4f9075",
    "slug": "title-co08ft",
    "body": "test comment uaiugs",
    "createdAt": 1582584705719,
    "updatedAt": 1582584705719,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment kulnnw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "875d53f6-15ff-4ddf-9ce0-1706c20d6d65",
    "slug": "title-co08ft",
    "body": "test comment kulnnw",
    "createdAt": 1582584705754,
    "updatedAt": 1582584705754,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-co08ft/comments

{
  "comment": {
    "body": "test comment f7ppuh"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "594dc26d-4f79-4ebe-bfe5-5863401f64a2",
    "slug": "title-co08ft",
    "body": "test comment f7ppuh",
    "createdAt": 1582584705782,
    "updatedAt": 1582584705782,
    "author": {
      "username": "commenter-vye4n8",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-co08ft/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-co08ft/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment slra9l"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-co08ft/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1582584705623,
      "id": "e10b7fa0-8d66-45f5-87ed-b81510e9f848",
      "body": "test comment x9jhso",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705623
    },
    {
      "createdAt": 1582584705593,
      "id": "533e1670-3d92-44f5-9e70-a331aae975df",
      "body": "test comment twjjte",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705593
    },
    {
      "createdAt": 1582584705719,
      "id": "92a6aa29-2f56-431c-b83e-47923a4f9075",
      "body": "test comment uaiugs",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705719
    },
    {
      "createdAt": 1582584705685,
      "id": "d35fab95-d2c5-4278-85c2-e104d87283eb",
      "body": "test comment 71sv83",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705685
    },
    {
      "createdAt": 1582584705782,
      "id": "594dc26d-4f79-4ebe-bfe5-5863401f64a2",
      "body": "test comment f7ppuh",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705782
    },
    {
      "createdAt": 1582584705754,
      "id": "875d53f6-15ff-4ddf-9ce0-1706c20d6d65",
      "body": "test comment kulnnw",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705754
    },
    {
      "createdAt": 1582584705490,
      "id": "169bccd9-a146-4a7a-9b43-852873c31fa8",
      "body": "test comment 26f3u0",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705490
    },
    {
      "createdAt": 1582584705559,
      "id": "a96e20f6-ec32-45fb-b533-50f3f52f7f3e",
      "body": "test comment oaieo8",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705559
    },
    {
      "createdAt": 1582584705652,
      "id": "fbe7e984-6107-4e6a-a6f3-8a813fc695eb",
      "body": "test comment y72p20",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705652
    },
    {
      "createdAt": 1582584705522,
      "id": "7b662d80-b479-4ae6-95be-cc5743d4a33e",
      "body": "test comment hgi10d",
      "slug": "title-co08ft",
      "author": {
        "username": "commenter-vye4n8",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1582584705522
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-co08ft/comments/169bccd9-a146-4a7a-9b43-852873c31fa8
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-co08ft/comments/7b662d80-b479-4ae6-95be-cc5743d4a33e
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-vye4n8]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-co08ft/comments/7b662d80-b479-4ae6-95be-cc5743d4a33e
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-co08ft/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "username": "user1-0.d4sfc2kric",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc",
    "username": "user1-0.d4sfc2kric",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "username": "user1-0.d4sfc2kric",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.d4sfc2kric]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.d4sfc2kric@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.d4sfc2kric@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc",
    "username": "user1-0.d4sfc2kric",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.ei8yqilmnwf",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.ei8yqilmnwf]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "password": "0.adqave440fl"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.d4sfc2kric@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc",
    "username": "user1-0.d4sfc2kric",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.d4sfc2kric
```
```
200 OK

{
  "profile": {
    "username": "user1-0.d4sfc2kric",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.g4qgqywzm54
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.g4qgqywzm54]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1ODI1ODQ3MDYsImV4cCI6MTU4Mjc1NzUwNn0.IS70NFePOZrOzFbYLiSeJmkXAYHdhmM_zrxDr5s6Usg",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.v3vjxo0ych",
    "email": "user2-0.v3vjxo0ych@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.v3vjxo0ych@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAudjN2anhvMHljaCIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.RuaEgKAghF67F0H1_Xmtne5ap51eViQPOXCmAFeG-mw",
    "username": "user2-0.v3vjxo0ych",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.d4sfc2kric@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.d4sfc2kric",
    "email": "updated-user1-0.d4sfc2kric@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.d4sfc2kric",
    "email": "updated-user1-0.d4sfc2kric@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.d4sfc2kric",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.d4sfc2kric",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuZDRzZmMya3JpYyIsImlhdCI6MTU4MjU4NDcwNiwiZXhwIjoxNTgyNzU3NTA2fQ.mUGyKcLloQJT71loi0gdqKWtkeyKTPCG0k5oK2zmKxc"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.637ebm5vskg@email.com",
    "username": "user2-0.637ebm5vskg",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.637ebm5vskg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuNjM3ZWJtNXZza2ciLCJpYXQiOjE1ODI1ODQ3MDYsImV4cCI6MTU4Mjc1NzUwNn0.ffxijgEfG_jPGiqlgBzpY-UaUF2ovM1IhWzvWTQ6r7s",
    "username": "user2-0.637ebm5vskg",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.637ebm5vskg@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.637ebm5vskg@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-02-24T22:51:46.725Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
