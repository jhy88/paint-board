DrawArea 설명

DrawArea 클래스는 JComponent를 상속받아 사용자 인터페이스를 구성하는 그리기 영역을 정의합니다.
image: 그림을 그릴 BufferedImage 객체입니다.
g2: 그래픽을 그리기 위한 Graphics2D 객체입니다.
prevX, prevY, currX, currY: 이전과 현재 마우스 위치를 저장하는 변수들입니다.
currentShape: 현재 선택된 도형의 종류를 나타내는 문자열입니다. 초기 값은 "Free Draw"입니다.
currentColor: 현재 그리기에 사용할 색상을 저장하는 변수입니다. 초기 값은 검은색(Color.BLACK)입니다.
currentStroke: 현재 그리기 선의 굵기를 저장하는 변수입니다. 초기 값은 1입니다.

DrawArea 클래스의 생성자에서는 기본적인 설정과 마우스 이벤트 처리를 초기화합니다.
setDoubleBuffered(false);: 더블 버퍼링을 비활성화하여 그림을 더 직접적으로 제어할 수 있게 합니다.
addMouseListener와 addMouseMotionListener: 마우스 이벤트를 처리하는 리스너를 등록합니다. mousePressed, mouseReleased, mouseDragged 등의 메서드로 마우스 이벤트가 발생할 때의 동작을 정의합니다.
mousePressed: 마우스 버튼이 눌릴 때의 동작을 정의합니다. 현재 좌표를 prevX, prevY에 저장합니다.
mouseReleased: 마우스 버튼이 떼어질 때의 동작을 정의합니다. 선택된 도형이 "Free Draw"나 "Eraser"가 아닐 경우 실제 도형을 그리고 화면을 다시 그립니다.
mouseDragged: 마우스 버튼이 눌린 채 움직일 때의 동작을 정의합니다. "Free Draw"나 "Eraser" 모드에서는 마우스가 움직이는 동안 선을 그리고 화면을 다시 그립니다.

paintComponent 메서드: 컴포넌트가 다시 그려질 때 호출되며, 실제 그림을 그리는 메서드입니다.
image가 초기화되지 않았다면 새로운 BufferedImage를 생성하고 초기화합니다.
g2에 대해 안티앨리어싱을 설정하여 부드러운 그림을 그릴 수 있도록 합니다.
clear() 메서드를 호출하여 이미지를 초기화하고, image를 화면에 그립니다.
선택된 도형 모드가 "Free Draw"나 "Eraser"가 아니면 선택된 도형을 그립니다.

clear() 메서드: 그림을 모두 지우고 초기화합니다.
setColor(Color color): 현재 색상을 변경하고 g2에 색상을 설정합니다.
setEraser(): 지우개 모드를 설정하고 g2에 흰색을 설정합니다.
setShape(String shape): 그릴 도형 모드를 설정하고, 지우개 모드가 아닌 경우 g2에 현재 색상을 설정합니다.
setStroke(int stroke): 선의 굵기를 설정하고 g2에 굵기를 설정합니다.
drawShape(int x1, int y1, int x2, int y2) 및 drawShape(Graphics2D g2d, int x1, int y1, int x2, int y2): 선택된 도형에 따라 선을 그리는 메서드입니다. drawShape(Graphics2D g2d, ...)는 실제로 도형을 그리는 작업을 합니다.

Main 클래스 설명
Main 클래스는 JFrame을 상속받아 애플리케이션의 메인 프레임을 정의합니다.
drawArea: 그림을 그릴 영역을 나타내는 DrawArea 객체입니다.
여러 JButton 객체들: 그림판의 다양한 기능(클리어, 색상 변경, 지우개, 선 그리기, 사각형 그리기, 타원 그리기, 자유 그리기)을 구현합니다.
JSlider: 선의 굵기를 조절하기 위한 슬라이더입니다.
currentColor: 현재 색상을 나타내는 변수입니다.
currentShape: 현재 선택된 도형의 종류를 나타내는 문자열입니다.
currentStroke: 현재 선의 굵기를 나타내는 변수입니다.

Main 생성자: JFrame을 초기화하고 컴포넌트들을 설정합니다.
setTitle("Java Paint");: 창의 제목을 "Java Paint"로 설정합니다.
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);: 창을 닫을 때 애플리케이션이 종료되도록 설정합니다.
setSize(800, 600);: 창의 크기를 800x600으로 설정합니다.
drawArea = new DrawArea();: 그림 그릴 영역을 초기화합니다.
각 JButton에 대한 설정:
clearBtn: "Clear" 버튼을 클릭하면 그림 영역을 지웁니다.
colorBtn: "Color" 버튼을 클릭하면 색상 선택 대화 상자가 나타납니다.
eraseBtn: "Eraser" 버튼을 클릭하면 지우개 모드로 전환합니다.
lineBtn, rectBtn, ovalBtn, freeDrawBtn: 각 버튼을 클릭하면 해당 도형 모드로 전환합니다.
strokeSlider: 슬라이더를 사용하여 선의 굵기를 조절할 수 있습니다. 슬라이더가 변경되면 currentStroke 값을 업데이트하고 그림 영역의 선 굵기를 설정합니다.
JPanel panel = new JPanel();: 버튼들과 슬라이더를 담을 패널을 생성하고 각 컴포넌트를 추가합니다.
add(panel, BorderLayout.NORTH);: 패널을 JFrame의 북쪽에 추가합니다.
add(drawArea, BorderLayout.CENTER);: 그림 그릴 영역을 JFrame의 중앙에 추가합니다.

main 메서드: 애플리케이션의 시작점입니다.
SwingUtilities.invokeLater: 새로운 스레드를 생성하여 Main 인스턴스를 만들고, 애플리케이션 창을 표시합니다.

즉, 이 프로그램을 요약하면 Main 클래스는 그림판 애플리케이션의 메인 프레임을 구성하며, 다양한 버튼과 슬라이더를 통해 그림 그리기, 색상 변경, 지우기, 도형 그리기 등의 기능을 제공합니다. DrawArea 클래스와 함께 작동하여 사용자 인터페이스와 그리기 기능을 구현합니다
