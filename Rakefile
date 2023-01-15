desc 'download source files'
task :download do
  32.times {|i|
    ext = i == 0 ? 'pdf' : 'zip'
    fn = "27-#{sprintf('%02d', i + 1)}.#{ext}"
    url = "https://www.city.nagaoka.niigata.jp/shisei/cate10/gis/file/#{fn}"
    sh <<-EOS
ts curl -o src/#{fn} --retry 5 #{url}
    EOS
  }
end

desc 'decompress files'
task :decompress do
  1.upto(32) {|i|
    fn = "27-#{sprintf('%02d', i)}.zip"
    sh <<-EOS
ts unar src/#{fn}
    EOS
  }
end

desc 'merge files into a single COG file'
task :merge do
  sh <<-EOS
gdalwarp -of COG -co COMPRESS=JPEG \
-s_srs EPSG:6676 -overwrite files/*.jpg nagaoka.tif
  EOS
end
