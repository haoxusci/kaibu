<template>
  <div id="comments-outside">
    <div class="comments-header">
      <div class="post-owner">
        <div class="avatar">
          <img :src="initial_comment.avatar" alt="" :title="initial_comment.user">
        </div>
        <div class="username">
          <a href="#">@{{ initial_comment.user }}</a>
        </div>
      </div>
      <div class="comments-stats">
        <span><i class="fa fa-thumbs-up"></i> {{ initial_comment.likes }}</span>
        <span><i class="fa fa-comment"></i> {{ comments.length }}</span>
      </div>
    </div>
    <comments
      :comments_wrapper_classes="['custom-scrollbar', 'comments-wrapper']"
      :comments="comments"
      :current_user="current_user"
      @submit-comment="submitComment"
    ></comments>
  </div>
</template>

<script>
import Comments from './Comments.vue'
export default {
  el: '#comments-session',
  name: "CommentBox",
  components: {
    Comments
  },
  //props: {'comments': Array},
  data() {
    return {
      initial_comment:{
        likes: 15,
        user: 'creator',
        avatar: 'http://via.placeholder.com/100x100/a74848',
        content: 'this is the first comment'   
      },
      current_user: {
        avatar: 'http://via.placeholder.com/100x100/a74848',
        user: 'hao',
      },
      comments: [
        {
          id: 1,
          user: 'user2',
          avatar: 'http://via.placeholder.com/100x100/a74848',
          content: 'comment from user2',
        }
      ]
    }
  },
  methods: {
    submitComment: function(reply) {
      this.comments.push({
        id: this.comments.length + 1,
        user: this.current_user.user,
        avatar: this.current_user.avatar,
        content: reply
      });
    },
    removeComment: function (comment){
      this.comments = this.comments.filter(
        function(ele){
          return ele != comment;
        }
      )
    }
  },
    
  //filters: {
  //  marked: marked
  //}
}
</script>
<style scoped>
*{
    padding: 0;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
}

#demo{
    margin: 20px 0 0 0;
}

.comment-form{
    display: block;
    width: 80%;
    margin: auto;
}

textarea{
    width: 100%;
    border: 2px solid #ccc;
    border-radius: 7px;
    height: 70px;
    font-family: Verdana, Helvetica, sans-serif;
    padding: 5px;
}

input{
    border: 2px solid #ccc;
    border-radius: 5px;
    padding: 5px;
}

button{
    background: #333;
    color: #ccc;
    border: 0;
    padding: 5px;
    cursor: pointer;
}

/*Comment Box*/

.comments-box{
    width: 90%;
    margin: auto;
    padding: 20px 0;
    border-bottom: 1px solid #000;
}

.delete-comment{
    background: red;
    color: #fff;
    font-size: 10px;
    cursor: pointer;
    display: inline;
    padding: 3px;
}

.user{
    margin: 10px 0;
    font-weight: bold;
}

a {
  text-decoration: none;
}
hr {
  display: block;
  height: 1px;
  border: 0;
  border-top: 1px solid #ececec;
  margin: 1em 0;
  padding: 0;
}
.comments-outside {
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
  margin: 0 auto;
  max-width: 600px;
}
.comments-header {
  background-color: #C8C8C8;
  padding: 10px;
  align-items: center;
  display: flex;
  justify-content: space-between;
  color: #333;
  min-height: 80px;
  font-size: 20px;
}
.comments-header .comments-stats span {
  margin-left: 10px;
}
.post-owner {
  display: flex;
  align-items: center;
}
.post-owner .avatar > img {
  width: 30px;
  height: 30px;
  border-radius: 100%;
}
.post-owner .username {
  margin-left: 5px;
}
.post-owner .username > a {
  color: #333;
}
</style>
