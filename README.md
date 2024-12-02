import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

void main() {
  runApp(JNVMemoryApp());
}

class JNVMemoryApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'JNV MEMORY',
      theme: ThemeData(
        primarySwatch: Colors.blueGrey,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  List<XFile>? _imageFiles = [];

  final ImagePicker _picker = ImagePicker();

  Future<void> pickImage() async {
    final List<XFile>? selectedImages = await _picker.pickMultiImage();
    if (selectedImages != null && selectedImages.isNotEmpty) {
      setState(() {
        _imageFiles!.addAll(selectedImages);
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('JNV MEMORY'),
        centerTitle: true,
      ),
      body: Column(
        children: [
          Expanded(
            child: _imageFiles == null || _imageFiles!.isEmpty
                ? Center(
                    child: Text(
                      'No images selected!',
                      style: TextStyle(fontSize: 18),
                    ),
                  )
                : GridView.builder(
                    gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                      crossAxisCount: 2,
                      crossAxisSpacing: 8.0,
                      mainAxisSpacing: 8.0,
                    ),
                    itemCount: _imageFiles!.length,
                    itemBuilder: (context, index) {
                      return Card(
                        child: Image.file(
                          File(_imageFiles![index].path),
                          fit: BoxFit.cover,
                        ),
                      );
                    },
                  ),
          ),
          SizedBox(height: 10),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              ElevatedButton(
                onPressed: pickImage,
                child: Text('Add Images'),
              ),
              ElevatedButton(
                onPressed: () {
                  Navigator.push(
                    context,
                    MaterialPageRoute(builder: (_) => TemplateCreationPage()),
                  );
                },
                child: Text('Create Template'),
              ),
            ],
          ),
        ],
      ),
    );
  }
}

class TemplateCreationPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Create Your Template'),
      ),
      body: Center(
        child: Text(
          'Template Creation Features Coming Soon!',
          style: TextStyle(fontSize: 18),
        ),
      ),
    );
  }
}
