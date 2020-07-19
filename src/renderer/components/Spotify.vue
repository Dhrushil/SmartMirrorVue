<template>
  
</template>


<script>
export default {
    mounted() {
        var request = require("request");
        var user_id = "matt"
        var token = "Bearer"
        var playlists_url="https://api.spotify.com/v1/users/"+user_id+"/playlists"

        request({url:playlist_url, headers:{"Authorization":token}}, function(err, res) {
            if (res) {
                var playlists=JSON.parse(res.body);
                var playlist_url = playlists.items[0].href
                request({url:playlist_url, headers:{"Authorization":token}}, function(err, res) {
                    if (res) {
                        var playlist = JSON.parse(res.body);
                        console.log("playlist: "+playlist.name)
                        playlist.tracks.forEach(function(track){
                            console.log(track.track.name);
                        })
                    }
                })
            }
        })


    }
}
</script>
<style>

</style>