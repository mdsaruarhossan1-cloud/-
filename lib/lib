import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

void main() {
  runApp(const SahityaApp());
}

class SahityaApp extends StatefulWidget {
  const SahityaApp({super.key});

  @override
  State<SahityaApp> createState() => _SahityaAppState();
}

class _SahityaAppState extends State<SahityaApp> {
  bool _isDarkMode = false;

  void _toggleTheme() {
    setState(() {
      _isDarkMode = !_isDarkMode;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'সাহিত্য কানন',
      themeMode: _isDarkMode ? ThemeMode.dark : ThemeMode.light,
      theme: ThemeData(
        useMaterial3: true,
        brightness: Brightness.light,
        colorSchemeSeed: const Color(0xFF673AB7),
        textTheme: GoogleFonts.tiroBanglaTextTheme(ThemeData.light().textTheme),
      ),
      darkTheme: ThemeData(
        useMaterial3: true,
        brightness: Brightness.dark,
        colorSchemeSeed: const Color(0xFFD1C4E9),
        textTheme: GoogleFonts.tiroBanglaTextTheme(ThemeData.dark().textTheme),
      ),
      home: MainNavigationHolder(onThemeToggle: _toggleTheme, isDarkMode: _isDarkMode),
    );
  }
}

class MainNavigationHolder extends StatefulWidget {
  final VoidCallback onThemeToggle;
  final bool isDarkMode;

  const MainNavigationHolder({super.key, required this.onThemeToggle, required this.isDarkMode});

  @override
  State<MainNavigationHolder> createState() => _MainNavigationHolderState();
}

class _MainNavigationHolderState extends State<MainNavigationHolder> {
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    final pages = [
      HomeScreen(onThemeToggle: widget.onThemeToggle, isDarkMode: widget.isDarkMode),
      const CategoryScreen(),
      const AuthorPanelScreen(),
      const ReaderScreen(bookTitle: 'নষ্ট নীড়', author: 'রবীন্দ্রনাথ ঠাকুর'),
      const ProfileScreen(),
    ];

    return Scaffold(
      body: pages[_currentIndex],
      bottomNavigationBar: NavigationBar(
        selectedIndex: _currentIndex,
        onDestinationSelected: (index) => setState(() => _currentIndex = index),
        destinations: const [
          NavigationDestination(icon: Icon(Icons.home_outlined), selectedIcon: Icon(Icons.home), label: 'হোম'),
          NavigationDestination(icon: Icon(Icons.category_outlined), selectedIcon: Icon(Icons.category), label: 'ক্যাটাগরি'),
          NavigationDestination(icon: Icon(Icons.edit_note_outlined), selectedIcon: Icon(Icons.edit_note), label: 'লেখক প্যানেল'),
          NavigationDestination(icon: Icon(Icons.menu_book_outlined), selectedIcon: Icon(Icons.menu_book), label: 'পড়ুন'),
          NavigationDestination(icon: Icon(Icons.person_outline), selectedIcon: Icon(Icons.person), label: 'প্রোফাইল'),
        ],
      ),
    );
  }
}

// =================১. হোম স্ক্রিন=================
class HomeScreen extends StatelessWidget {
  final VoidCallback onThemeToggle;
  final bool isDarkMode;

  const HomeScreen({super.key, required this.onThemeToggle, required this.isDarkMode});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('সাহিত্য কানন', style: TextStyle(fontWeight: FontWeight.bold)),
        actions: [
          IconButton(
            icon: Icon(isDarkMode ? Icons.light_mode : Icons.dark_mode),
            onPressed: onThemeToggle,
          ),
          IconButton(icon: const Icon(Icons.notifications_none), onPressed: () {}),
        ],
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAlignment.start,
          children: [
            // সার্চ বার
            TextField(
              decoration: InputDecoration(
                hintText: 'বই বা লেখক খুঁজুন...',
                prefixIcon: const Icon(Icons.search),
                border: OutlineInputBorder(borderRadius: BorderRadius.circular(30)),
                filled: true,
              ),
            ),
            const SizedBox(height: 20),

            // প্রিমিয়াম ব্যানার
            Container(
              padding: const EdgeInsets.all(16),
              decoration: BoxDecoration(
                gradient: const LinearGradient(colors: [Colors.purple, Colors.deepPurple]),
                borderRadius: BorderRadius.circular(16),
              ),
              child: Row(
                children: [
                  const Expanded(
                    child: Column(
                      crossAxisAlignment: CrossAlignment.start,
                      children: [
                        Text('প্রিমিয়াম মেম্বারশিপ', style: TextStyle(color: Colors.white, fontSize: 18, fontWeight: FontWeight.bold)),
                        SizedBox(height: 4),
                        Text('বিজ্ঞাপনমুক্ত অফলাইন রিডিং ও অডিও বুক সুবিধা পান।', style: TextStyle(color: Colors.white70, fontSize: 12)),
                      ],
                    ),
                  ),
                  ElevatedButton(
                    onPressed: () {},
                    style: ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                    child: const Text('সাবস্ক্রাইব', style: TextStyle(color: Colors.black, fontWeight: FontWeight.bold)),
                  )
                ],
              ),
            ),
            const SizedBox(height: 20),

            const Text('AI রিকমেন্ডেশন', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            const SizedBox(height: 10),
            SizedBox(
              height: 160,
              child: ListView(
                scrollDirection: Axis.horizontal,
                children: [
                  _buildBookCard('পথের পাঁচালী', 'বিভূতিভূষণ', Colors.orange),
                  _buildBookCard('গীতাঞ্জলি', 'রবীন্দ্রনাথ ঠাকুর', Colors.teal),
                  _buildBookCard('হিমু রিমান্ডে', 'হুমায়ূন আহমেদ', Colors.yellow[800]!),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildBookCard(String title, String author, Color color) {
    return Container(
      width: 120,
      margin: const EdgeInsets.only(right: 12),
      padding: const EdgeInsets.all(12),
      decoration: BoxDecoration(color: color.withOpacity(0.2), borderRadius: BorderRadius.circular(12)),
      child: Column(
        crossAxisAlignment: CrossAlignment.start,
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          const Icon(Icons.book, size: 40),
          const Spacer(),
          Text(title, style: const TextStyle(fontWeight: FontWeight.bold), maxLines: 1),
          Text(author, style: const TextStyle(fontSize: 12, color: Colors.grey), maxLines: 1),
        ],
      ),
    );
  }
}

// =================২. ক্যাটাগরি স্ক্রিন=================
class CategoryScreen extends StatelessWidget {
  const CategoryScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final categories = [
      {'name': 'উপন্যাস', 'icon': Icons.menu_book, 'color': Colors.blue},
      {'name': 'গল্প', 'icon': Icons.auto_stories, 'color': Colors.green},
      {'name': 'কবিতা', 'icon': Icons.history_edu, 'color': Colors.purple},
      {'name': 'ইসলামিক বই', 'icon': Icons.mosque, 'color': Colors.teal},
      {'name': 'শিশু সাহিত্য', 'icon': Icons.child_care, 'color': Colors.orange},
      {'name': 'বিজ্ঞান ও ইতিহাস', 'icon': Icons.science, 'color': Colors.red},
    ];

    return Scaffold(
      appBar: AppBar(title: const Text('বইয়ের ক্যাটাগরি')),
      body: GridView.builder(
        padding: const EdgeInsets.all(16),
        gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2, crossAxisSpacing: 12, mainAxisSpacing: 12, childAspectRatio: 1.3,
        ),
        itemCount: categories.length,
        itemBuilder: (context, index) {
          final item = categories[index];
          return Card(
            color: (item['color'] as Color).withOpacity(0.1),
            child: InkWell(
              onTap: () {},
              borderRadius: BorderRadius.circular(12),
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(item['icon'] as IconData, size: 40, color: item['color'] as Color),
                  const SizedBox(height: 8),
                  Text(item['name'] as String, style: const TextStyle(fontWeight: FontWeight.bold, fontSize: 16)),
                ],
              ),
            ),
          );
        },
      ),
    );
  }
}

// =================৩. ই-বুক রিডার স্ক্রিন (Interactive Reader)=================
class ReaderScreen extends StatefulWidget {
  final String bookTitle;
  final String author;

  const ReaderScreen({super.key, required this.bookTitle, required this.author});

  @override
  State<ReaderScreen> createState() => _ReaderScreenState();
}

class _ReaderScreenState extends State<ReaderScreen> {
  double _fontSize = 16.0;
  Color _bgColor = Colors.white;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: _bgColor,
      appBar: AppBar(
        title: Text(widget.bookTitle),
        actions: [
          IconButton(icon: const Icon(Icons.bookmark_add_outlined), onPressed: () {}),
          IconButton(
            icon: const Icon(Icons.text_fields),
            onPressed: () {
              showModalBottomSheet(
                context: context,
                builder: (context) => Container(
                  padding: const EdgeInsets.all(20),
                  height: 180,
                  child: Column(
                    children: [
                      const Text('ফন্ট সাইজ ও ব্যাকগ্রাউন্ড অ্যাডজাস্টমেন্ট'),
                      Slider(
                        value: _fontSize,
                        min: 12, max: 28,
                        onChanged: (val) => setState(() => _fontSize = val),
                      ),
                      Row(
                        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                        children: [
                          _buildBgBtn(Colors.white, 'হালকা'),
                          _buildBgBtn(const Color(0xFFF5E6D3), 'সেপিয়া'),
                          _buildBgBtn(Colors.grey[900]!, 'ডার্ক'),
                        ],
                      )
                    ],
                  ),
                ),
              );
            },
          ),
        ],
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(20),
        child: Text(
          'এখানে বইয়ের মূল লেখা প্রদর্শিত হবে। পাঠক তার পছন্দমতো ফন্ট সাইজ বড়-ছোট করতে পারবেন এবং নাইট মোড বা সেপিয়া ব্যাকগ্রাউন্ডে স্বাচ্ছন্দ্যে পড়তে পারবেন। শেষ কোথায় পড়া হয়েছে অ্যাপ তা স্বয়ংক্রিয়ভাবে মনে রাখবে।',
          style: TextStyle(fontSize: _fontSize, height: 1.6, color: _bgColor == Colors.grey[900] ? Colors.white : Colors.black),
        ),
      ),
    );
  }

  Widget _buildBgBtn(Color color, String label) {
    return ElevatedButton(
      style: ElevatedButton.styleFrom(backgroundColor: color),
      onPressed: () => setState(() => _bgColor = color),
      child: Text(label, style: const TextStyle(color: Colors.blueAccent)),
    );
  }
}

// =================৪. লেখক প্যানেল=================
class AuthorPanelScreen extends StatelessWidget {
  const AuthorPanelScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('লেখক প্যানেল')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            ElevatedButton.icon(
              onPressed: () {},
              icon: const Icon(Icons.cloud_upload),
              label: const Text('নতুন বই/অধ্যায় আপলোড করুন'),
              style: ElevatedButton.styleFrom(minimumSize: const Size.fromHeight(50)),
            ),
            const SizedBox(height: 20),
            const Align(
              alignment: Alignment.centerLeft,
              child: Text('পাঠকদের মন্তব্য ও রেটিং', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            ),
            const SizedBox(height: 10),
            Expanded(
              child: ListView(
                children: const [
                  ListTile(
                    leading: CircleAvatar(child: Text('আ')),
                    title: Text('আরিফ হোসেন'),
                    subtitle: Text('দারুণ গল্প! পরবর্তী অধ্যায়ের অপেক্ষায় রইলাম।'),
                    trailing: Text('⭐ 5.0'),
                  ),
                ],
              ),
            )
          ],
        ),
      ),
    );
  }
}

// =================৫. ইউজার প্রোফাইল ও স্ট্যাটিস্টিকস=================
class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('আমার প্রোফাইল')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            const CircleAvatar(radius: 40, child: Icon(Icons.person, size: 50)),
            const SizedBox(height: 10),
            const Text('ইউজার নাম', style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
            const Text('user@email.com', style: TextStyle(color: Colors.grey)),
            const SizedBox(height: 20),

            // রিডিং স্ট্যাটিস্টিকস
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              children: [
                _buildStatTile('পড়া হয়েছে', '১২টি বই'),
                _buildStatTile('মোট সময়', '২৪ ঘন্টা'),
                _buildStatTile('পয়েন্ট', '৪৫০'),
              ],
            ),
            const Divider(height: 40),
            ListTile(leading: const Icon(Icons.download), title: const Text('অফলাইন ডাউনলোডসমূহ'), onTap: () {}),
            ListTile(leading: const Icon(Icons.share), title: const Text('রেফারেল ও আয়'), onTap: () {}),
            ListTile(leading: const Icon(Icons.admin_panel_settings), title: const Text('অ্যাডমিন প্যানেল'), onTap: () {}),
          ],
        ),
      ),
    );
  }

  Widget _buildStatTile(String title, String value) {
    return Column(
      children: [
        Text(value, style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold, color: Colors.deepPurple)),
        Text(title, style: const TextStyle(fontSize: 12, color: Colors.grey)),
      ],
    );
  }
}
