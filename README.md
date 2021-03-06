It can be used with apache upload progress module, nginx upload progress module or lighttpd, read more here: http://drogomir.com/blog/2008/6/18/upload-progress-bar-with-mod_passenger-and-apache

## Usage

some html:
     <form id="upload" enctype="multipart/form-data" action="index.html" method="post">
        <input name="file" type="file"/>
        <input type="submit" value="Upload"/>
      </form>

      <div id="uploading">
        <div id="progress" class="bar">
          <div id="progressbar">&nbsp;</div>
          <div id="percents"></div>
        </div>
      </div>

then some css:

    .bar {
      width: 300px;
    }

    #progress {
      background: #eee;
      border: 1px solid #222;
      margin-top: 20px;
    }
    #progressbar {
      width: 0px;
      height: 24px;
      background: #333;
    }

and a bit of javascript:

    $(function() {
      $('form').uploadProgress({
        /* scripts locations for safari */
        jqueryPath: "../lib/jquery.js",
        uploadProgressPath: "../jquery.uploadProgress.js",
        /* function called each time bar is updated */
        uploading: function(upload) {$('#percents').html(upload.percents+'%');},
        /* selector or element that will be updated */
        progressBar: "#progressbar",
        /* progress reports url */
        progressUrl: "/progress",
        /* how often will bar be updated */
        interval: 2000
      });
    });

If you need to update the progress bar from a different domain or subdomain, liek if your upload server is different from your normal web server, you can try the JSON-P protocol, like this:

    $(function() {
      $('form').uploadProgress({
        /* scripts locations for safari */
        jqueryPath: "../lib/jquery.js",
        uploadProgressPath: "../jquery.uploadProgress.js",
        /* function called each time bar is updated */
        uploading: function(upload) {$('#percents').html(upload.percents+'%');},
        /* selector or element that will be updated */
        progressBar: "#progressbar",
        /* progress reports url in a different domain or subdomain from caller */
        progressUrl: "uploads.somewhere.com/progress",
        /* how often will bar be updated */
        interval: 2000,
        /* use json-p for cross-domain call */
        dataType: 'jsonp'
      });
    });

defaults:

    interval: 2000
    progressBar: "#progressbar"
    progressUrl: "/progress"
    start: function() {}
    uploading: function() {}
    complete: function() {}
    success: function() {}
    error: function() {}
    uploadProgressPath: '/javascripts/jquery.js'
    jqueryPath: '/javascripts/jquery.uploadProgress.js'
    dataType: 'json'

## License

Ruby on Rails is released under the [MIT License](http://www.opensource.org/licenses/MIT).
