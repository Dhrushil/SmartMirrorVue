<template>
  <div><button id="authorize_button" style="display: none;">Authorize</button>
    <button id="signout_button" style="display: none;">Sign Out</button>
</div>
</template>

<script>
export default {
  data: ()=> ({
    CLIENT_ID : '1059733584205-t3gtvnfommrc6n654va43cdgo81bqjvd.apps.googleusercontent.com',
      API_KEY : 'AIzaSyDIvtq_DBb2j6F-TJdR3RjiXlnZBgY6vdg',
      DISCOVERY_DOCS: [
        "https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest"
      ],
      SCOPES: "https://www.googleapis.com/auth/calendar.readonly",
  }),
  methods: {
    handleClientLoad() {
        gapi.load('client:auth2', this.initClient);
    },
    initClient() {
      gapi.client.init({
        apiKey: this.API_KEY,
        clientId: this.CLIENT_ID,
        discoveryDocs: this.DISCOVERY_DOCS,
        scope: this.SCOPES
      }).then(function() {
        gapi.auth2.getAuthInstance().isSignedIn.listen(updateSigninStatus);

          // Handle the initial sign-in state.
          this.updateSigninStatus(gapi.auth2.getAuthInstance().isSignedIn.get());
          this.authorizeButton.onclick = this.handleAuthClick;
          this.signoutButton.onclick = this.handleSignoutClick;

      }, function(error) {
        appendPre(JSON.stringify(error, null, 2));
      });
    },
    updateSigninStatus(isSignedIn) {
      if (isSignedIn) {
          this.authorizeButton.style.display = 'none';
          this.signoutButton.style.display = 'block';
          listLabels();
        } else {
          this.authorizeButton.style.display = 'block';
          this.signoutButton.style.display = 'none';
        }
    },
    handleAuthClick(event) {
      gapi.auth2.getAuthInstance().signIn();
    },
    handleSignoutClick(event) {
      gapi.auth2.getAuthInstance().signOut();
    },
    appendPre(message) {
        var pre = document.getElementById('content');
        var textContent = document.createTextNode(message + '\n');
        pre.appendChild(textContent);
      },
      listLabels() {
        gapi.client.gmail.users.labels.list({
          'userId': 'me'
        }).then(function(response) {
          var labels = response.result.labels;
          appendPre('Labels:');

          if (labels && labels.length > 0) {
            for (i = 0; i < labels.length; i++) {
              var label = labels[i];
              appendPre(label.name)
            }
          } else {
            appendPre('No Labels found.');
          }
        });
      },
      mounted () {
         var authorizeButton = document.getElementById('authorize_button');
         var signoutButton = document.getElementById('signout_button');
          this.handleClientLoad();


      }


  }
};
</script>

