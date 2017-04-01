# Jarvee

# Text detect for Traffic sign.

This is just the part of text localization.

Briefly it processes in this order:

ER algorithm extracts possible candidates and then specificly judged by a CNN network generated by caffe.

For effeciency demand the CNN network is the same as mnist net in caffe samples...

This project requests Ubuntu,opencv3,caffe and consists of three parts.

The caffe_model/ contains the CNN network,img/ contains labeled image,and the other code is the main.cpp and its support function.

# Let me specificly explain how this code work....

1,main.cpp loads img and its labels from img/label_img_data.txt
2,For each pic ,ER extracts possible candidates.
3,Compare the candidates with labeled region and if matches output this pitches into train/has/ or val/has/,otherwise into train/no/ or val/no.And see the cover rate.(Sadly I only get about 0.9.I don't know in details how lots of paper got nearly 1.0...)
4,Run create_image_net.sh to create lmdb,make_imagenet_mean.sh to make mean data,and train.sh and wait a long time...Common caffe process.
5,But after 10,000 iterations I only got 0.9 precision...
6,Run main.cpp again,after extracting candidates see in int prediction(Mat img) which calls caffe API to judge if this candidate has a char.
7,Finally calculate all the indexes.

# To run this code you need to change these abosolute path by your own 

in main.cpp...

string data_path = "/home/cpdp/lijiahui/svm/img/";
string caffe_path = "/home/cpdp/lijiahui/caffe/caffe-master/data/myself/";
char * label_path = "/home/cpdp/lijiahui/svm/img/label.txt";
char * train_txt = "/home/cpdp/lijiahui/caffe/caffe-master/data/myself/train.txt";
char * test_txt = "/home/cpdp/lijiahui/caffe/caffe-master/data/myself/val.txt";

and this command to call your own caffe prediction process.

string command = "/home/cpdp/lijiahui/caffe/caffe-master/build/examples/cpp_classification/classification1.bin \
  /home/cpdp/lijiahui/caffe/caffe-master/data/myself/deploy.prototxt \
  /home/cpdp/lijiahui/caffe/caffe-master/data/myself/snapshot_iter_1000.caffemodel \
  /home/cpdp/lijiahui/caffe/caffe-master/data/myself/imagenet_mean.binaryproto \
  /home/cpdp/lijiahui/caffe/caffe-master/data/myself/word.txt \ ";

and in read_data.cpp this path: FILE *fp = fopen("/home/cpdp/lijiahui/svm/img/label_img_data.txt", "r");

and in caffe_model/ lots of path in ".sh" files..

and in img/ two ".txt" files, open them you will know how to change.




