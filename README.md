exif-as3
========

Exif reading library for AS3. You can find the specification at http://www.exif.org/Exif2-2.PDF.

Examples
========

Display thumbnail image
-----------------------

The following code displays original JPEG image and thumbnail image.

    import jp.shichiseki.exif.*;
    
    var loader:ExifLoader = new ExifLoader();
    
    private function loadImage():void {
      loader.addEventListener(Event.COMPLETE, onComplete);
      loader.load(new URLRequest("http://www.example.com/sample.jpg"));
    }
    
    private function onComplete(e:Event):void {
      // display image
      addChild(loader);
      // display thumbnail image
      var thumbLoader:Loader = new Loader();
      thumbLoader.loadBytes(loader.exif.thumbnailData);
      addChild(thumbLoader);
    }

Show Exif IFD informations
--------------------------

The following code shows Exif IFD information.

    import jp.shichiseki.exif.*;
    
    var loader:ExifLoader = new ExifLoader();
    
    private function loadImage():void {
      loader.addEventListener(Event.COMPLETE, onComplete);
      loader.load(new URLRequest("http://www.example.com/sample.jpg"));
    }
    
    private function onComplete(e:Event):void {
      if (loader.exif.ifds.primary)
        displayIFD(loader.exif.ifds.primary);
      if (loader.exif.ifds.exif)
        displayIFD(loader.exif.ifds.exif);
      if (loader.exif.ifds.gps)
        displayIFD(loader.exif.ifds.gps);
      if (loader.exif.ifds.interoperability)
        displayIFD(loader.exif.ifds.interoperability);
      if (loader.exif.ifds.thumbnail)
        displayIFD(loader.exif.ifds.thumbnail);
    }
    
    private function displayIFD(ifd:IFD):void {
      trace(" --- " + ifd.level + " --- ");
      for (var entry:String in ifd) {
        trace(entry + ": " + ifd[entry]);
      }
    }

Lisence
=======

MIT-license.
