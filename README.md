public class account extends JFrame {
	
	JLabel lblUser;
	JTextField tfUser;
	JLabel lblPass;
	JTextField tfPass;
	JButton btnRegist;
	//tạo đối tượng connect
	Connection conn;
	Statement stmt;
	//tạo hàm connect DB
	public void connectDB() {
		try {
			Class.forName("com.mysql.jdbc.Driver");
			conn = DriverManager.getConnection("jdbc:mysql://localhost/StudentDB", "root", "");
			System.out.println("Connect Success");		
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
		}
	}

	public account() {
		lblUser = new JLabel("User Name");
		tfUser = new JTextField(10);
		lblPass = new JLabel("Password");
		tfPass = new JTextField(10);
		btnRegist = new JButton("Regist");
		btnRegist.addActionListener (new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				// TODO Auto-generated method stub
				try {
					connectDB();
					stmt = (Statement) conn.createStatement();
							int n = stmt.executeUpdate("Insert into Account values('"+tfUser.getText()+"','"+tfPass.getText()+"')");
							if (n>0) JOptionPane.showMessageDialog(null,"Success");
							else JOptionPane.showMessageDialog(null,"Fail");
				} catch (Exception e2) {
					// TODO: handle exception
				}
				
			}
		});
		setLayout(new FlowLayout());
		setSize(300,200);
		Container cont = this.getContentPane();
		cont.add(lblUser);
		cont.add(tfUser);
		cont.add(lblPass);
		cont.add(tfPass);
		cont.add(btnRegist);
		setVisible(true);
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new account();
	}

}
