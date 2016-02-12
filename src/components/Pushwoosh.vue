<template>
  <div class="hello">
    <h1>{{ msg }}</h1>


    <div class="box box-primary direct-chat direct-chat-primary">
      <div class="box-header with-border">
        <h3 class="box-title">Direct Chat</h3>

        <div class="box-tools pull-right">
          <span data-toggle="tooltip" title="3 New Messages" class="badge bg-light-blue">3</span>
          <button type="button" class="btn btn-box-tool" data-widget="collapse"><i class="fa fa-minus"></i>
          </button>
          <button type="button" class="btn btn-box-tool" data-toggle="tooltip" title="Contacts" data-widget="chat-pane-toggle">
            <i class="fa fa-comments"></i></button>
          <button type="button" class="btn btn-box-tool" data-widget="remove"><i class="fa fa-times"></i></button>
        </div>
      </div>
      <!-- /.box-header -->
      <div class="box-body">
        <!-- Conversations are loaded here -->
        <div class="direct-chat-messages" v-for="notifications in notification">
          <!-- Message. Default to the left -->
          <div class="direct-chat-msg">
            <div class="direct-chat-info clearfix">
              <span class="direct-chat-name pull-left">Pushwoosh</span>
              <span class="direct-chat-timestamp pull-right">{{ day }}</span>
            </div>
            <!-- /.direct-chat-info -->
            <img class="direct-chat-img" src="bower_components/AdminLTE/dist/img/user1-128x128.jpg" alt="Message User Image"><!-- /.direct-chat-img -->
            <div class="direct-chat-text">
              {{ notification.message }}
            </div>
            <!-- /.direct-chat-text -->
          </div>
          <!-- /.direct-chat-msg -->


        </div>
        <!--/.direct-chat-messages-->

        <!-- Contacts are loaded here -->
        <div class="direct-chat-contacts">
          <ul class="contacts-list">
            <li>
              <a href="#">
                <img class="contacts-list-img" src="bower_components/AdminLTE/dist/img/user1-128x128.jpg">

                <div class="contacts-list-info">
                            <span class="contacts-list-name">
                              Count Dracula
                              <small class="contacts-list-date pull-right">2/28/2015</small>
                            </span>
                  <span class="contacts-list-msg">How have you been? I was...</span>
                </div>
                <!-- /.contacts-list-info -->
              </a>
            </li>
            <!-- End Contact Item -->
          </ul>
          <!-- /.contatcts-list -->
        </div>
        <!-- /.direct-chat-pane -->
      </div>
      <!-- /.box-body -->
      <div class="box-footer">
        <div class="input-group">
          <input id="notification" type="text" name="message" placeholder="Type Message ..." class="form-control">
                  <span class="input-group-btn">
                    <button v-on:click="notify" type="button" class="btn btn-primary btn-flat">Send</button>
                  </span>
        </div>
      </div>
      <!-- /.box-footer-->
    </div>

  </div>
</template>

<script>
  export default {
    data:function () {
      return {
        // note: changing this line won't causes changes
        // with hot-reload because the reloaded component
        // preserves its current state and we are modifying
        // its initial state.
        msg: 'Hello World!',
        notification_message : "Notification per defecte",
        notifications : [
          { message: 'Foo', date: 'Now'},
          { message: 'Bar', date: '2 minuts ago'}
        ]
      }
    },
    methods:{
      notify() {
    var notification= $('#notification').val()
    $.ajax({
      type: "POST",
      url: "https://cp.pushwoosh.com/json/1.3/createMessage",
      data: JSON.stringify({
        "request": {
          "application": "4FC89B6D14A655.46488481",
          "auth": "mTdns0j6qLYPa/A5htmD46xVyoxdVQfPBz7NRqYYHz9PhvKXgJtOkAY+yo0YTXDEoztQAJFY0JmXnd89tf59",
          "notifications": [{
            "send_date": "now",
            "ignore_user_timezone": true,
            "content": notification
          }]
        }
      }),
      dataType: "json"
    }).done(function(data) {
      console.log(data);
    });
  }
  }
  }
</script>
