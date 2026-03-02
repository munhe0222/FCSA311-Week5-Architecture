# FCSA311-Week5-Architecture
1. Программ ба Системийн ялгаа
1.1 Тодорхойлолт

Программ (Program) гэдэг нь тодорхой нэг асуудлыг шийдэх зорилготой бичигдсэн кодын цуглуулга юм. Ихэнхдээ нэг executable файл эсвэл нэг application байдаг.

Систем (System) гэдэг нь олон програм, сервер, өгөгдлийн сан, хэрэглэгч, бизнес процесс зэргийг хамарсан иж бүрэн бүтэц юм.

Программ бол нэг хэсэг. Систем бол олон хэсгийн нэгдэл.

1.2 Харьцуулсан хүснэгт
Үзүүлэлт	Программ	Систем
Хэмжээ	Жижиг	Том
Бүтэц	Нэг кодын сан	Олон дэд систем
Зорилго	Нэг үйлдэл	Бизнесийн иж бүрэн шийдэл
Жишээ	Calculator	Banking System
1.3 Бодит жишээ
Жишээ 1: Calculator App

Зөвхөн тооцоолол хийдэг

Database шаардлагагүй

Нэг хэрэглэгч ашиглана

Жишээ 2: E-Commerce System

Web application

Mobile application

Payment service

Database

Admin panel

2. Архитектур гэж юу вэ?
2.1 Өөрийн үгээр тодорхойлолт

Архитектур гэдэг нь програм эсвэл системийн бүтцийг урьдчилан төлөвлөж, компонентууд хэрхэн холбогдож, өгөгдөл хэрхэн урсахыг тодорхойлсон загвар юм.

Архитектургүй систем нь замбараагүй баригдсан байшинтай адил.

2.2 Архитектурын үндсэн компонентууд

UI Layer

Business / Service Layer

Data Access Layer

Database

2.3 Dependency чиглэл
UI  →  Service  →  Repository  →  Database

UI нь Service-г дуудна

Service нь Repository ашиглана

Repository нь Database-тэй холбогдоно

Доод layer нь дээд layer-ийг мэдэхгүй

2.4 Technology Decision

Архитектурын үед дараах шийдвэрүүдийг гаргана:

Programming language (Java, C#, Python гэх мэт)

Framework (Spring, .NET, Django)

Database (MySQL, PostgreSQL, MongoDB)

Deployment (Cloud эсвэл On-premise)

Monolith эсвэл Microservice

3. Layered Architecture
3.1 Тайлбар

Layered Architecture нь системийг логик давхаргад хувааж, хариуцлагыг ялгадаг загвар юм.

3.2 Архитектур Diagram

|       UI Layer    |

          ↓

|    Service Layer  |

          ↓

|  Repository Layer |

          ↓

|      Database     |

3.3 Web Application Жишээ (Python Flask)
Project Structure
project/
 app.py
 service.py
 repository.py
 templates/
repository.py
class UserRepository:
    def get_user(self, user_id):
        return {"id": user_id, "name": "Bat"}
service.py
from repository import UserRepository

class UserService:
    def __init__(self):
        self.repository = UserRepository()

    def get_user_name(self, user_id):
        user = self.repository.get_user(user_id)
        return user["name"]
app.py (UI Layer)
from flask import Flask
from service import UserService

app = Flask(__name__)
service = UserService()

app.route("/user/<int:id>")
def get_user(id):
    return service.get_user_name(id)

if __name__ == "__main__":
    app.run(debug=True)

 UI зөвхөн Service дуудах
 Service бизнес логик агуулна
 Repository өгөгдөлтэй ажиллана

4. Low Coupling & High Cohesion
4.1 Low Coupling

Компонентууд хоорондоо бага хамааралтай байх.

 Нэг layer өөр layer-ийн дотоод кодыг мэдэхгүй
 Өөрчлөлт хийхэд бүх систем нурж унахгүй

4.2 High Cohesion

Нэг class нэг зорилготой байх.

 UserService зөвхөн user-тэй холбоотой логик
 PaymentService зөвхөн төлбөрийн логик

4.3 Муу архитектурын жишээ
class System:
    def get_user(self):
        pass

    def send_email(self):
        pass

    def calculate_salary(self):
        pass

 Нэг class бүх ажлыг хийж байна
 Low cohesion
 High coupling

4.4 Сайн архитектурын жишээ
class UserRepository:
    pass

class EmailService:
    pass

class SalaryService:
    pass

 Хариуцлага тусдаа
 Өргөтгөх боломжтой
 Засварлахад амар

5. Дүгнэлт
Архитектур яагаад чухал вэ?

Системийг ойлгомжтой болгоно

Том системийг удирдах боломжтой болгоно

Багийн хөгжүүлэлтэд тохиромжтой

Засвар, өргөтгөл хийхэд хялбар

Performance болон security-д нөлөөлнө

Сайн архитектур = Урт хугацааны чанартай систем
