##		 安裝

###		Windows

###	1.環境	
	pip install virtualenv 
	virtualenv flask	#flask是名稱
	在位置下執行activate
	pip install flask
	以及打flask可以看到如何執行

!(https://github.com/BarryFu/flask/blob/master/picutre/1.JPG)

###	2.Hello
	from flask import Flask    #先定義名稱Flask及格式flask
	app = Flask(__name__)      #變數

	@app.route('/')    #位置       
	def hello_world():
   		return 'Hello World'

### 3.不同名稱不同位置
	from flask import Flask
	app = Flask(__name__)
	
	@app.route('/hello/<name>')  #給他位置在hello底下及不同變數(名字)，可以根據目的來分配位置
	def hello_name(name):
	   return 'Hello %s!' % name  #根據輸入的變數(名字),輸出Hello 字串
	
	if __name__ == '__main__':
	   app.run(debug = True)

!(https://github.com/BarryFu/flask/blob/master/picutre/3.JPG)

### 4.製作html、按鈕
	<html>		#頭尾是html格式及內文開始
	   	<body>  
	   		   <form action = "http://localhost:5000/login" method = "post">	   		   #給這個html的位置login用
	   		   
	   		      <p>Enter Name:</p>			說明字串
	   		      <p><input type = "text" name = "nm" /></p>	#可以輸入變數nm的名稱，等等在flask裡面會用到
	   		      <p><input type = "submit" value = "submit" /></p>		#叫submit的按鈕
	   		   </form>   
	 	</body>
	</html>	

	另外html <br> 標籤代表的是換一行，而 <p> 標籤則會換兩行

!(https://github.com/BarryFu/flask/blob/master/picutre/4.JPG)

### 5.呼叫nm裡面的名稱
	from flask import Flask, redirect, url_for, request		#因為跟html有相互關係必須呼叫
	app = Flask(__name__)
	
	@app.route('/success/<name>')		
	def success(name):
	   return 'welcome %s' % name
	
	@app.route('/login',methods = ['POST', 'GET'])
	def login():
	   if request.method == 'POST':
	      user = request.form['nm']
	      return redirect(url_for('success',name = user))
	   else:
	      user = request.args.get('nm')
	      return redirect(url_for('success',name = user))
	
	if __name__ == '__main__':
	   app.run(debug = True)

!(https://github.com/BarryFu/flask/blob/master/picutre/5.JPG)