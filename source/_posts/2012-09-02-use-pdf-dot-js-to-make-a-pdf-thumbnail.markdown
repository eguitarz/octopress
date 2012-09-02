---
layout: post
title: "Use pdf.js to make a PDF thumbnail"
date: 2012-09-02 08:52
comments: true
categories: 
---
If you want to make a PDF cover image, what will you do? Grab a monster library just only for making thumbnail? No, you don't. It's dead easy to go with [pdf.js](https://github.com/mozilla/pdf.js).

cavas.html.haml
    !!!
    %html
      %head
        %script{:src => "javascripts/pdf.js", :type => "text/javascript"}
      %body
        :javascript
          'use strict';

          PDFJS.workerSrc = "javascripts/pdf.js";
          $(document).ready(function() {
            PDFJS.getDocument('iperl.pdf').then(function(pdf){
             
              pdf.getPage(1).then(function(page) {
                var viewport = page.getViewport(0.5);
                var canvas = document.getElementById('box');
                var ctx = canvas.getContext('2d');
                canvas.height = viewport.height;
                canvas.width = viewport.width;

                var renderContext = {
                  canvasContext: ctx,
                  viewport: viewport
                };

                page.render(renderContext).then(function(){
                  //set to draw behind current content
                  ctx.globalCompositeOperation = "destination-over";
              
                  //set background color
                  ctx.fillStyle = "#ffffff";
              
                  //draw background / rect on entire canvas
                  ctx.fillRect(0,0,canvas.width,canvas.height);
                  var img = canvas.toDataURL();
                  $("#thumbnail").html('<img src="'+img+'"/>');
                });
               
              });
            });
           
          })
      #thumbnail
      %canvas#box{:style => "border:1px solid black;background-color: white;"}/

The result contains an image and a canvas, quite simple, isn't it?
