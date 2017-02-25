#MVC 란?
Model-View-Controller를 말한다.
어플리케이션을 3개의 로직으로 분류해서 구성하는 것이다.

##model
오브젝트 혹은 데이터를 말한다.
view와 controller 사이를 오가는 데이터, 데이터에 적용되는 관련된 룰이다.
view에서 불러오는 데이터.
controller의 지시에 따라 업데이트 되기도 한다.
데이터가 바뀌면 controller를 업데이트 하기도 한다.

    public class Student {
       private String rollNo;
       private String name;

       public String getRollNo() {
          return rollNo;
       }

       public void setRollNo(String rollNo) {
          this.rollNo = rollNo;
       }

       public String getName() {
          return name;
       }

       public void setName(String name) {
          this.name = name;
       }
    }

##view
UI로직을 말한다.
    public class StudentView {
        public void printStudentDetails(String studentName, String studentRollNo){
          System.out.println("Student: ");
          System.out.println("Name: " + studentName);
          System.out.println("Roll No: " + studentRollNo);
        }
    }


##controller
- model과 view사이에서 중개자 역할은 한다.
- model에서 view로 가는 data flow를 관리한다.
- model의 데이터를 가지고 작업을 해서 view에 최종 화면을 출력한다.
예) view의 input폼에 사용자가 입력한 데이터를 model을 사용해서 데이터베이스에 저장한다.

    public class StudentController {
        private Student model;
        private StudentView view;

        public StudentController(Student model, StudentView view){
          this.model = model;
          this.view = view;
        }

        public void setStudentName(String name){
          model.setName(name);		
        }

        public String getStudentName(){
          return model.getName();		
        }

        public void setStudentRollNo(String rollNo){
          model.setRollNo(rollNo);		
        }

        public String getStudentRollNo(){
          return model.getRollNo();		
        }

        public void updateView(){				
          view.printStudentDetails(model.getName(), model.getRollNo());
        }
    }

##예제
###온라인 서점
1. 사용자가 '판타지'라고 검색창에 입력한다.
2. controller는 요청(get, post)을 받는다.
3. controller는 요청의 파라미터를 읽어서, model에 해당하는 데이터를 달라고 한다.
4. model은 데이터베이스에서 데이터를 가져온다. (이때, 필요하면 필터를 적용한다거나 하는 로직을 적용한다.)
5. controller는 해당하는 view에 데이터를 보내준다. (모바일 기기면 모바일 view, 스킨이 설정되 있다면 해당하는 스킨의 view 등)

### 결론은, 똑같은 데이터를 controller가 상황에 맞게 다른 view를 선택해서 랜더링 해준다.
