from flask import Flask, request, jsonify
import pymysql

app = Flask(__name__)


# 데이터베이스 연결
db = pymysql.connect(
    host="127.0.0.1",
    user="root",
    password="sion@12345",
    db="camerainfo",
    charset="utf8mb4",
    cursorclass=pymysql.cursors.DictCursor
)
@app.route('/location_status', methods=['GET'])
def location_status():
    
    with db.cursor() as cursor:
        query = "SELECT location, status FROM camerainfo"
        cursor.execute(query)
        result = cursor.fetchall()
        
    if result:
        return jsonify(result)

# Mac 주소를 기반으로 ExternalIP 및 Port 정보 가져오기
@app.route('/get_externalIP_port', methods=['POST','GET'])
def get_externalIP_port():
    macAddr = request.args.get('macAddr')

    with db.cursor() as cursor:
        query = f"SELECT macAddr, externalIP, port FROM camerainfo WHERE macAddr = '{macAddr}'"
        cursor.execute(query)
        result = cursor.fetchone()

    if result:
        return jsonify(result)
    else:
        return jsonify({})

if __name__ == '__main__':
    app.run(debug=True)