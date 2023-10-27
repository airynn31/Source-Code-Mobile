# Source-Code-Mobile
Merupakan source code dalam bahasa pemrograman flutter mengenai validasi input pada formulir untuk memenuhi tugas UTS pada mata kuliah Pemrograman Sistem Mobile Universitas Sultan Ageng Tirtayasa 2023-2024


(Code Main.dart)
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    const appTitle = 'Validate Form';

  return MaterialApp(
      title: appTitle,
      home: Scaffold(
        appBar: AppBar(
          title: const Text(appTitle),
          backgroundColor: const Color.fromARGB(255, 139, 76, 175),
        ),
        body: const MyCustomForm(),
      ),
    );
  }
}

class MyCustomForm extends StatefulWidget {
  const MyCustomForm({super.key});
  static TextEditingController password = TextEditingController();
  static TextEditingController confirmpassword = TextEditingController();


  @override
  MyCustomFormState createState() => MyCustomFormState();
}

class MyCustomFormState extends State<MyCustomForm> {

  final _formKey = GlobalKey<FormState>();

  var passToggle = true;

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          CircleAvatar(
            radius: 70,
            child: Image.network("https://protocoderspoint.com/wp-content/uploads/2020/10/PROTO-CODERS-POINT-LOGO-water-mark-.png"),
          ),
          const SizedBox(
            height: 15,
            ),
      Padding(
            padding: const EdgeInsets.only(bottom: 15,left: 10,right: 10),
            child: TextFormField( 
              autofocus: true,
              decoration: const InputDecoration(
                hintText: 'Name',
                labelText: 'Full name',
                icon: Icon(Icons.people)),
              validator: (value) {
                if (value == null || !RegExp(r'^[a-z A-Z]+$').hasMatch(value!)) {
                  return 'Input your full name!';
                }else{
                  return null;
              }
              }
            ),
          ),
      Padding(
            padding: const EdgeInsets.only(bottom: 15,left: 10,right: 10),
            child: TextFormField(
              decoration: const InputDecoration(
                hintText: 'Email',
                labelText: 'Email',
                icon: Icon(Icons.email)),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Input your valid email!';
                } else if (!value.contains('@gmail.com')) {
                  return 'Unvalidated Email';
                }
                return null;
              },
            ),
          ),
      Padding(
            padding: const EdgeInsets.only(bottom: 15,left: 10,right: 10),
            child: TextFormField(
              decoration: const InputDecoration(
                hintText: 'Phone Number',
                labelText: 'Phone',
                icon: Icon(Icons.phone)),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Input your phone number!';
                } else if (!value.contains('08')) {
                  return 'Unvalidated Phone Number';
                }
                return null;
              },
            ),
          ),
      Padding(
            padding: const EdgeInsets.only(bottom: 15,left: 10,right: 10),
            child: TextFormField(
              controller: MyCustomForm.password,
              obscureText: passToggle,
              decoration: InputDecoration(
                hintText: 'Your password',
                labelText: 'Password',
                icon: const Icon(Icons.lock),
                suffix: InkWell(
                  onTap: () {
                    setState(() {
                      passToggle = !passToggle;
                    });
                  },
                  child: Icon(
                      passToggle ? Icons.visibility : Icons.visibility_off),
                )),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Make your password within 8 characters';
                }
                if (value.length < 8) {
                  return 'Minimal 8 characters';
                }
                return null;
              },
          ),
          ),
      Padding(
            padding: const EdgeInsets.only(bottom: 15,left: 10,right: 10),
            child: TextFormField(
              controller: MyCustomForm.confirmpassword,
              obscureText: passToggle,
              decoration: InputDecoration(
                hintText: 'Your password',
                labelText: 'Confirm Password',
                icon: const Icon(Icons.lock),
                suffix: InkWell(
                  onTap: () {
                    setState(() {
                      passToggle = !passToggle;
                    });
                  },
                  child: Icon(
                      passToggle ? Icons.visibility : Icons.visibility_off),
                )),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Re-input your new password!';
                }
                print(MyCustomForm.password.text);
                print(MyCustomForm.confirmpassword.text);
                if(MyCustomForm.password.text!=MyCustomForm.confirmpassword.text){
                  return "Password does not match!";
                }
                return null;
              },
          ),
          ),
      Padding(
            padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
            child: ElevatedButton(
                style: ElevatedButton.styleFrom(
                  backgroundColor: const Color.fromARGB(255, 139, 76, 175),
                ),
                child: const Text('SUBMIT'),
                onPressed: () {
                  if (_formKey.currentState!.validate()) {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                          builder: (context) => const SecondRoute()),
                    );
                    ScaffoldMessenger.of(context).showSnackBar(
                      const SnackBar(content: Text('Succesfull')),
                    );
                  }
                }),
          ),
        ],
      ),
    );
  }
}

class SecondRoute extends StatelessWidget {
  const SecondRoute({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        backgroundColor: const Color.fromARGB(255, 139, 76, 175),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          style: ElevatedButton.styleFrom(
            backgroundColor: const Color.fromARGB(255, 139, 76, 175),
          ),
          child: const Text('Go Back'),
        ),
      ),
    );
  }
}
