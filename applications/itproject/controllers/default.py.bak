import random

def index():
    from random import randint
    pol = db(db.News.category=="Politics").select()
    sport = db(db.News.category=="Sports").select()
    busy = db(db.News.category=="Business").select()
    inter = db(db.News.category=="International").select()
    enter = db(db.News.category=="Entertainment").select()
    boly = db(db.News.category=="Bollywood").select()
    return locals()
def politics():
    pol = db(db.News.category=="Politics").select()
    var = request.args
    forms = {}
    for i in pol:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
def sports():
    sport = db(db.News.category=="Sports").select()
    var = request.args
    forms = {}
    for i in sport:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
def business():
    busy = db(db.News.category=="Business").select()
    var = request.args
    forms = {}
    for i in busy:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
def international():
    inter = db(db.News.category=="International").select()
    var = request.args
    forms = {}
    for i in inter:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
def entertainment():
    enter = db(db.News.category=="Entertainment").select()
    var = request.args
    forms = {}
    for i in enter:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
def bollywood():
    boly = db(db.News.category=="Bollywood").select()
    var = request.args
    forms = {}
    for i in boly:
        forms[i.id] = SQLFORM(db.News_comment,labels={'body':'Comment'})
        forms[i.id].vars.title = i.id
        forms[i.id].process()
    db.News_comment.title.readable=False
    db.News_comment.title.writable=False
    return locals()
@auth.requires_login()
def create():
    form = SQLFORM(db.Live_Updates).process()
    if form.accepted:
        redirect(URL('index'))
    return locals()


@auth.requires_membership('admins')
def manage():
    form1 = crud.create(db.News)
    form3 = crud.create(db.auth_user)
    form4 = crud.create(db.auth_group)
    form5 = crud.create(db.auth_membership)
    form6 = crud.create(db.auth_permission)
    grid2 = SQLFORM.smartgrid(db.News,csv=False,create=False)
    grid3 = SQLFORM.smartgrid(db.News_comment,csv=False,create=False)
    grid4 = SQLFORM.smartgrid(db.auth_user,csv=False,create=False)
    grid5 = SQLFORM.smartgrid(db.auth_group,csv=False,create=False)
    grid6 = SQLFORM.smartgrid(db.auth_membership,csv=False,create=False)
    grid7 = SQLFORM.smartgrid(db.auth_permission,csv=False,create=False)
    return locals()


def show():
    update = db.Live_Updates(request.args(0,cast=int))
    db.Blog_Comment.Live_Updates.default = update.id
    db.Blog_Comment.Live_Updates.readable = False
    db.Blog_Comment.Live_Updates.writable = False
    form = SQLFORM(db.Blog_Comment).process()
    comments = db(db.Blog_Comment.Live_Updates==update.id).select()
    return locals()


def user():
    """
    exposes:
    http://..../[app]/default/user/login
    http://..../[app]/default/user/logout
    http://..../[app]/default/user/register
    http://..../[app]/default/user/profile
    http://..../[app]/default/user/retrieve_password
    http://..../[app]/default/user/change_password
    http://..../[app]/default/user/manage_users (requires membership in
    use @auth.requires_login()
        @auth.requires_membership('group name')
        @auth.requires_permission('read','table name',record_id)
    to decorate functions that need access control
    """
    return dict(form=auth())


@cache.action()
def download():
    """
    allows downloading of uploaded files
    http://..../[app]/default/download/[filename]
    """
    return response.download(request, db)


def call():
    """
    exposes services. for example:
    http://..../[app]/default/call/jsonrpc
    decorate with @services.jsonrpc the functions to expose
    supports xml, json, xmlrpc, jsonrpc, amfrpc, rss, csv
    """
    return service()


@auth.requires_login()
def api():
    """
    this is example of API with access control
    WEB2PY provides Hypermedia API (Collection+JSON) Experimental
    """
    from gluon.contrib.hypermedia import Collection
    rules = {
        '<tablename>': {'GET':{},'POST':{},'PUT':{},'DELETE':{}},
        }
    return Collection(db).process(request,response,rules)
