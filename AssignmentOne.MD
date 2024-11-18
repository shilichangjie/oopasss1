```java
import java.util.ArrayList;

// "Part1:创建HealthProfessional";
class HealthProfessional {
    int id;
    String name;
    String description;

    // "默认的构造函数constructor";
    public HealthProfessional() {
    }

    // "初始化变量构造函数constructor";
    public HealthProfessional(int id, String name, String description) {
        this.id = id;
        this.name = name;
        this.description = description;
    }

    // "打印详情函数printDetails";
    public void printDetails() {
        System.out.println("Doctor ID: " + id);
        System.out.println("Doctor Name: " + name);
        System.out.println("Doctor Description: " + description);
    }
}

// "Part2:创建子类GeneralPractitioner";
class GeneralPractitioner extends HealthProfessional {

    // "默认的构造函数constructor";
    public GeneralPractitioner() {
    }

    // "初始化变量构造函数constructor,super经参数传递给父类";
    public GeneralPractitioner(int id, String name, String description) {
        super(id, name, description);
    }

    // "打印详情函数printDetails,super调用父类的方法输出所有信息printDetails";
    public void printDetails() {
        super.printDetails();
        System.out.println("Specialty: HealthProfessional");
    }
}

// "Part2:创建自定义子类Cardiologist";
class Cardiologist extends HealthProfessional {
    // "声明他的专业specialty";
    String specialty = "Cardiologist";

    // "默认的构造函数constructor";
    public Cardiologist() {

    }

    // "初始化变量构造函数constructor,super经参数传递给父类";
    public Cardiologist(int id, String name, String description) {
        super(id, name, description);
    }

    // "打印详情函数printDetails,super调用父类的方法输出所有信息printDetails";
    public void printDetails() {
        super.printDetails();
        System.out.println("Specialty: " + this.specialty);
    }
}

// "Part4:创建预约类Appointment";
class Appointment {

    String name;
    String phone;
    String time;
    HealthProfessional doctor;

    // "默认的构造函数constructor";
    public Appointment() {

    }

    // "初始化变量构造函数包含name,phone,time,doctor";
    public Appointment(String name, String phone, String time, HealthProfessional doctor) {
        this.name = name;
        this.phone = phone;
        this.time = time;
        this.doctor = doctor;
    }

    // "打印预约详情的函数printDetails";
    public void printDetails() {
        System.out.println("Name: " + name);
        System.out.println("Phone: " + phone);
        System.out.println("Time: " + time);
        doctor.printDetails();
    }
}

// "运行主类AssignmentOne";
public class AssignmentOne {
    // "Part5:声明appointmentList用于存储Appointment实例的ArrayList";
    static ArrayList<Appointment> appointmentList = new ArrayList<>();

    // "运行主函数main";
    public static void main(String[] args) {
        // "Part3:创建三名全科医生和两名其他类型的医疗专业人员";
        GeneralPractitioner General1 = new GeneralPractitioner(1, "Anna Taylor", "Family medicine specialist");
        GeneralPractitioner General2 = new GeneralPractitioner(2, "James Miller", "General health care provider");
        GeneralPractitioner General3 = new GeneralPractitioner(3, "Laura Wilson", "Focuses on preventive care");
        Cardiologist Cardiologist1 = new Cardiologist(4, "Sarah Lee", "Cardiovascular imaging specialist");
        Cardiologist Cardiologist2 = new Cardiologist(5, "Linda Davis", "Arrhythmia and pacemaker expert");
        // "Part3:输出全部医疗专业人员的信息用printDetails";
        General1.printDetails();
        System.out.println("------------------------------");
        General2.printDetails();
        System.out.println("------------------------------");
        General3.printDetails();
        System.out.println("------------------------------");
        Cardiologist1.printDetails();
        System.out.println("------------------------------");
        Cardiologist2.printDetails();
        System.out.println("------------------------------");

        // "Part5:添加2个全科医生和2个其他医生的预约用createAppointment";
        System.out.println("第五部分");
        createAppointment("Emma", "1234567890", "2024-11-11 9:00", General1);
        createAppointment("Henry", "2234567890", "2024-11-12 10:30", General2);
        createAppointment("Liam", "3234567890", "2024-11-13 11:00", Cardiologist1);
        createAppointment("Quinn", "4234567890", "2024-11-14 12:30", Cardiologist2);

        // "Part5:输出已预约的列表";
        printExistingAppointments();
        // "Part5:取消预约";
        cancelBooking("4234567890");
        // "Part5:取消后更新的预约列表";
        printExistingAppointments();
        // "Part5:取消不存在的";
        cancelBooking("1122334455");
    }

    // "Part5:创建预约createAppointment";
    public static void createAppointment(String name, String phone, String time, HealthProfessional doctor) {
        // "生成预约appointment";
        Appointment appointment = new Appointment(name, phone, time, doctor);
        // "添加到appointmentList用add";
        appointmentList.add(appointment);
        // "打印创建成功";
        System.out.println("create appointment success!");
    }

    // "Part5:输出已预约列表printExistingAppointments";
    public static void printExistingAppointments() {
        // "判断预约列表数量";
        if (appointmentList.size() == 0) {
            System.out.println("please add appointment");
        } else {
            // "不是空的就打印预约列表appointmentList";
            for (int i = 0; i < appointmentList.size(); i++) {
                appointmentList.get(i).printDetails();
                System.out.println("------------------------------");
            }
        }
    }

    // "Part5:取消预约cancelBooking";
    public static void cancelBooking(String phone) {
        boolean bool = false;
        for (int i = 0; i < appointmentList.size(); i++) {
            // "在预约列表里找是否有该手机号的预约equals比较phone是否相等;"
            if (appointmentList.get(i).phone == phone) {
                // "remove删除列表中该手机号的预约";
                appointmentList.remove(i);
                System.out.println("Cancel Success: " + phone);
                bool = true;
                break;
            }
        }
        // "如果bool是false说明预约列表没找phone取消失败;"
        if (!bool) {
            System.out.println("Cancel Error: " + phone);
        }
    }
}
```