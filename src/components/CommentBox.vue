<template>
  <div id="commentbox">
    <div class="comment-form">    
      <textarea type="text" v-model="comment" placeholder="Comment"></textarea>
      <label>
        <input type="text" v-model="author" placeholder="Author">
      </label>
      <button @click="addComment()">Add Comment</button>
    </div>
    <div v-for="comment in comments" :key=comment.id class="comments-box">
      <p class="author">
        {{comment.author}}: {{comment.content}}
      </p>
      <!--p v-html="content | marked" class="content-comment"></p-->
      <p @click="removeComment(comment)" class="delete">Delete</p>
    </div>
  </div>
</template>

<script>
export default {
  el: '#comments-session',
  name: "CommentBox",
  //props: ['comments'],
  //props: {'comments': Array},
  data() {
    return {comments: []}
  },
  methods: {
    addComment(){
      //e.preventDefault();
      const newComment = {
        id: new Date().getTime(),
        author: this.author,
        content: this.comment
      }
      if(this.author && this.comment){
        this.comments.push(newComment)
        console.log(this.comments)
      }else{
        alert('Fields Empty');
      }
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

.delete{
    background: red;
    color: #fff;
    font-size: 12px;
    cursor: pointer;
    display: inline;
    padding: 3px;
}

.author{
    margin: 10px 0;
    font-weight: bold;
}
</style>
