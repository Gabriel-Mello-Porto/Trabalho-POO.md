# Trabalho-POO

## Hero
```java
import javax.swing.*;

abstract class Hero {
    private int hp;
    private int atk;
    private int def;
    private ImageIcon portrait;

  
    public Hero(int hp, int atk, int def){
      this.hp = hp;
      this.atk = atk;
      this.def = def;
  }

    // getter setter
    public int getHp() {
        return hp;
    }

    public void setHp(int hp) {
        this.hp = hp;
    }

    public int getAtk() {
        return atk;
    }

    public void setAtk(int atk) {
        this.atk = atk;
    }

    public int getDef() {
        return def;
    }

    public void setDef(int def) {
        this.def = def;
    }

    // skill
    public abstract boolean useSkill();

    public ImageIcon getPortrait(){
        return portrait;
    }
}

```
### Gunslinger
```java
import javax.swing.*;

class Gunslinger extends Hero {

    ImageIcon portrait = new ImageIcon("src/imgs/Gunslinger.png");
    private boolean skill = true;

    public Gunslinger(int hp, int atk, int def) {
        super(10, 3, 2);
    }

    // skill
    @Override
    public boolean useSkill() {
        if (skill) {
            skill = false;
            return true;
        }
        return false;
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```

### Outlaw
```java
import javax.swing.*;
class Outlaw extends hero{

  ImageIcon portrait=new ImageIcon("src/imgs/Outlaw.png");
  private boolean skill=true;

  public Outlaw(int hp, int atk, int def){
      super(7,5,0);
  }

  //skill
  @Override
  public boolean useSkill() {
      if (skill) {
          skill = false;
          return true;   
      }
      return false;
  }

  public ImageIcon getPortrait() {
      return portrait;
  }
  
}
```

### Sheriff

```java
import javax.swing.*;

class Sheriff extends hero{

  ImageIcon portrait=new ImageIcon("src/imgs/Sheriff.png");
  private boolean skill=true;

  Sheriff(int hp, int atk, int def){
      super(13,2,6);
  }

  //skill
  @Override
  public boolean useSkill() {
      if (skill) {
          skill = false;
          return true;   
      }
      return false;
  }

  public ImageIcon getPortrait() {
      return portrait;
  }
}
```



## InimigoBasico
```java
public abstract class InimigoBasico {

    private String nome;
    private int hp;
    private int atk;
    private int def;

    public InimigoBasico(String nome, int hp, int atk, int def) {
        this.nome = nome;
        this.hp = hp;
        this.atk = atk;
        this.def = def;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getHp() {
        return hp;
    }

    public void setHp(int hp) {
        this.hp = hp;
    }

    public int getAtk(){
        return atk;
    }

    public void setAtk(int atk) {
        this.atk = atk;
    }

    public int getDef(){
        return def;
    }

    public void setDef(int def) {
        this.def = def;
    }
}
```

### Indio
```java
import javax.swing.ImageIcon;

public class Rogue extends InimigoBasico {

    ImageIcon portrait = new ImageIcon("");

    Rogue(String nome, int hp, int atk, int def) {
        super(nome, hp, atk, def);
    }

}
```

### Rogue
```java
import javax.swing.ImageIcon;

public class Indio extends InimigoBasico {

    ImageIcon portrait = new ImageIcon("");

    Indio(String nome, int hp, int atk, int def) {
        super(nome, hp, atk, def);
    }
}
```


## BillyTheKid (chefao)
```java
import javax.swing.ImageIcon;

public class BillyTheKid{

    ImageIcon portrait = new ImageIcon("");

    private int hp=20;
    private int atk=5;
    private int def=5;
    
    BillyTheKid(int hp, int atk, int def) {
        hp=this.hp;
        atk=this.atk;
        def=this.def;
    }

    public int getHp() {
        return hp;
    }

    void setHp(int hp) {
        hp = this.hp;
    }

    int getAtk() {
    return atk;
    }

    void setAtk(int atk) {
        atk = this.atk;
    }

    int getDef() {
        return def;
    }

    void setDef(int def) {
        def = this.def;
    }
}
```

## changebackground

```java
import java.awt.*;
import javax.swing.*;

class changebackground extends JPanel {
    private Image backgroundImage;


    public changebackground(String imagePath) {
        backgroundImage = new ImageIcon("src/imgs/Upgradescreen2.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Imagem de fundo
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```



## Backgroundimg
```java
import java.awt.*;
import javax.swing.*;

class backgroundimg extends JPanel {
    private Image backgroundImage;

    
    public backgroundimg(String imagePath) {
        backgroundImage = new ImageIcon("src/imgs/Coverart2.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Draw the background image
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```

## Hero screen

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.EmptyBorder;

class Hscreen extends JFrame implements ActionListener {

    // botões
    private JButton Bgunslinger;
    private JButton Boutlaw;
    private JButton Bsheriff;

    // icones
    ImageIcon gunslingerIcon;
    ImageIcon outlawIcon;
    ImageIcon sheriffIcon;

    public Hscreen() {
        super("Hero Selection");

        // icone da janale
        ImageIcon icon = new ImageIcon("src/imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        Container tela = getContentPane();
        setSize(800, 480);
        setLayout(new BorderLayout());

        // tamanho do botão
        Dimension buttonSize = new Dimension(148, 202);

        // escalar as imagens
        gunslingerIcon = scaleImageIcon(new ImageIcon("src/imgs/gunslingerbaner.png"), buttonSize.width,
                buttonSize.height);
        outlawIcon = scaleImageIcon(new ImageIcon("src/imgs/outlawbaner.png"), buttonSize.width, buttonSize.height);
        sheriffIcon = scaleImageIcon(new ImageIcon("src/imgs/sheriffbaner.png"), buttonSize.width, buttonSize.height);

        // botões ja re-escalados
        Bgunslinger = new JButton(gunslingerIcon);
        Boutlaw = new JButton(outlawIcon);
        Bsheriff = new JButton(sheriffIcon);

        // travar tamanho do botão
        Bgunslinger.setPreferredSize(buttonSize);
        Bgunslinger.setMinimumSize(buttonSize);
        Bgunslinger.setMaximumSize(buttonSize);

        Boutlaw.setPreferredSize(buttonSize);
        Boutlaw.setMinimumSize(buttonSize);
        Boutlaw.setMaximumSize(buttonSize);

        Bsheriff.setPreferredSize(buttonSize);
        Bsheriff.setMinimumSize(buttonSize);
        Bsheriff.setMaximumSize(buttonSize);

        // action listeners
        Bgunslinger.addActionListener(this);
        Boutlaw.addActionListener(this);
        Bsheriff.addActionListener(this);

        // imagem de fundo
        Hselect backimg = new Hselect("src/imgs/HSelectinfo.png");

        // painel de botões
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        buttonPanel.setOpaque(false); // fazer botão transparente
        buttonPanel.setBorder(new EmptyBorder(40, 0, 0, 0)); // espaço para baixo
        buttonPanel.add(Bgunslinger);
        buttonPanel.add(Boutlaw);
        buttonPanel.add(Bsheriff);

        // labels
        JLabel Lgunslinger = new JLabel(
                "<html>Gunslinger: An agile master of the revolvers <br> <strong>Skill:<strong> Trick Shot (Deals 50% more damage on the next shot)</html>");
        Lgunslinger.setForeground(Color.BLACK);
        Lgunslinger.setFont(new Font("Arial", Font.BOLD, 12));
        JLabel Loutlaw = new JLabel(
                "<html>Outlaw: A deadly rogue, master in dodging the law <br> <strong>Skill:<strong> Footwork (Dodges next attack)</html>");
        Loutlaw.setForeground(Color.BLACK);
        Loutlaw.setFont(new Font("Arial", Font.BOLD, 12));
        JLabel Lsheriff = new JLabel(
                "<html>Sheriff: The law incarnate, not many can escape his neverending pursuit <br> <strong> Skill:<strong> Prof Of Justice (Take only half the damage for the next attack)</html>");
        Lsheriff.setForeground(Color.BLACK);
        Lsheriff.setFont(new Font("Arial", Font.BOLD, 12));

        JPanel labelPanel = new JPanel();
        labelPanel.setLayout(new BoxLayout(labelPanel, BoxLayout.Y_AXIS));
        labelPanel.setOpaque(false);
        labelPanel.setBorder(new EmptyBorder(60, 180, 0, 0)); // Espaço para baixo e direita
        labelPanel.add(Lgunslinger);
        labelPanel.add(Box.createRigidArea(new Dimension(0, 10))); // espaço entre as labels
        labelPanel.add(Loutlaw);
        labelPanel.add(Box.createRigidArea(new Dimension(0, 10))); // espaço entre as labels
        labelPanel.add(Lsheriff);

        backimg.setLayout(new BorderLayout());
        backimg.add(buttonPanel, BorderLayout.NORTH);
        backimg.add(labelPanel, BorderLayout.CENTER);

        // adicionando info
        tela.add(backimg, BorderLayout.CENTER);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent action) {
        if (action.getSource() == Bgunslinger) {
            
            Gunslinger gunslinger = new Gunslinger(10, 3, 2);
            ChScreen chScreen = new ChScreen(gunslinger);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            
        }
        if (action.getSource() == Boutlaw) {

            Outlaw outlaw = new Outlaw(7, 5, 0);
            ChScreen chScreen = new ChScreen(outlaw);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            
        }
        if (action.getSource() == Bsheriff) {

            Sheriff sheriff = new Sheriff(13, 2, 6);
            ChScreen chScreen = new ChScreen(sheriff);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            
        }
    }

    // resizer de imagem
    private ImageIcon scaleImageIcon(ImageIcon icon, int width, int height) {
        Image img = icon.getImage();
        Image scaledImg = img.getScaledInstance(width, height, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

}
```


## Hselect
```java
import java.awt.*;
import javax.swing.*;

class Hselect extends JPanel {
    private Image backgroundImage;


    public Hselect(String imagePath) {
        backgroundImage = new ImageIcon("src/imgs/HSelectinfo.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Imagem de fundo
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```


## Mwindows
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class Mwindows extends JFrame implements ActionListener {

  private JButton Bstart;
  private JButton Bdebug;
  private JButton Bexit;

  public Mwindows() {
    super("Wild West Crusade");

    // Icone
    ImageIcon icon = new ImageIcon("src/imgs/WWC2icon.png");
    setIconImage(icon.getImage());

    Container tela = getContentPane();
    setSize(800, 480);
    setLayout(new BorderLayout());

    // botões
    Bstart = new JButton("New Game");
    Bdebug = new JButton("Debug");
    Bexit = new JButton("Exit");

    // leitores para botões
    Bstart.addActionListener(this);
    Bdebug.addActionListener(this);
    Bexit.addActionListener(this);

    // Imagem de fundo
    backgroundimg backimg = new backgroundimg("src/imgs/Coverart2.png");

    // painel de botões
    JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
    buttonPanel.setOpaque(false); // background dos botões transparente
    buttonPanel.add(Bstart);
    buttonPanel.add(Bdebug);
    buttonPanel.add(Bexit);

    // adicionando os elemntos na tela
    backimg.setLayout(new BorderLayout());
    backimg.add(buttonPanel, BorderLayout.SOUTH);

    // adicionando a imagem
    tela.add(backimg, BorderLayout.CENTER);

    setVisible(true);
  }

  public void actionPerformed(ActionEvent action) {
    if (action.getSource() == Bstart) {

      Hscreen Hscreen = new Hscreen();

      Hscreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

    }
    
    if (action.getSource() == Bdebug) {
      
      Hscreen Hscreen = new Hscreen();
      Hscreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

    }
    if (action.getSource() == Bexit) {

      JOptionPane.showMessageDialog(this, "Exiting the game", "Info", JOptionPane.INFORMATION_MESSAGE, null);

      System.exit(0);
    }

  }
}
```


## Chscreen 
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.EmptyBorder;

class ChScreen extends JFrame implements ActionListener {

    // botões
    private JButton hpp;
    private JButton hpm;

    private JButton atkp;
    private JButton atkm;

    private JButton defp;
    private JButton defm;

    private JButton Bconfirm;

    private JLabel heroname;
    private JLabel infohp;
    private JLabel infoatk;
    private JLabel infodef;
    private JLabel pointsLabel;

    private ImageIcon picture;

    private Hero character;

    public int points = 10;

    public ChScreen(Hero character) {
        super("Character Customization");
        this.character = character;

        // icone de janela
        ImageIcon icon = new ImageIcon("src/imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        Container tela = getContentPane();
        setSize(800, 480);
        setLayout(new BorderLayout());

        changebackground backimg = new changebackground("src/imgs/Upgradescreen2.png");
        backimg.setLayout(null);

        Dimension buttonSize = new Dimension(80, 30);

        // inicialização
        hpp = new JButton("HP+");
        hpp.setSize(buttonSize);

        hpm = new JButton("HP-");
        hpm.setSize(buttonSize);

        atkp = new JButton("ATK+");
        atkp.setSize(buttonSize);

        atkm = new JButton("ATK-");
        atkm.setSize(buttonSize);

        defp = new JButton("DEF+");
        defp.setSize(buttonSize);

        defm = new JButton("DEF-");
        defm.setSize(buttonSize);

        Bconfirm = new JButton("Confirm");
        Bconfirm.setSize(100, 30);

        // listeners
        hpp.addActionListener(this);
        hpm.addActionListener(this);
        atkp.addActionListener(this);
        atkm.addActionListener(this);
        defp.addActionListener(this);
        defm.addActionListener(this);

        // labels
        String name = character.getClass().getSimpleName();
        heroname = new JLabel("" + name);
        heroname.setForeground(Color.BLACK);

        infohp = new JLabel("HP: " + character.getHp(), SwingConstants.CENTER);
        infohp.setForeground(Color.BLACK);

        infoatk = new JLabel("ATK: " + character.getAtk(), SwingConstants.CENTER);
        infoatk.setForeground(Color.BLACK);

        infodef = new JLabel("DEF: " + character.getDef(), SwingConstants.CENTER);
        infodef.setForeground(Color.BLACK);

        pointsLabel = new JLabel("Points Left: " + points, SwingConstants.CENTER);
        pointsLabel.setForeground(Color.BLACK);

        // imagem de personagem
        picture = scaleImageIcon(character);
        JLabel Lportrait = new JLabel(picture);
        // posição e tamanho da imagem
        Lportrait.setBounds(446, 90, 200, 200);

        // painel de botões
        JPanel buttonPanel = new JPanel(new GridLayout(4, 2, 20, 20));
        buttonPanel.setOpaque(false);
        buttonPanel.setBounds(60, 80, 250, 300);

        // Adding buttons and labels to the button panel
        buttonPanel.add(hpm);
        buttonPanel.add(infohp);
        buttonPanel.add(hpp);

        buttonPanel.add(atkm);
        buttonPanel.add(infoatk);
        buttonPanel.add(atkp);

        buttonPanel.add(defm);
        buttonPanel.add(infodef);
        buttonPanel.add(defp);

        // posição do confirm
        Bconfirm.setBounds(140, 380, 100, 30);
        // posição dos labels
        pointsLabel.setBounds(60, 300, 250, 30);
        heroname.setBounds(146, 55, 250, 30);

        // adicionando elementos na tela
        backimg.add(buttonPanel);
        backimg.add(Bconfirm);
        backimg.add(Lportrait);
        backimg.add(pointsLabel);
        backimg.add(heroname);

        // imagem de fundo
        tela.add(backimg, BorderLayout.CENTER);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent action) {
        if (action.getSource() == hpp && points > 0) {
            character.setHp(character.getHp() + 1);
            points--;
        } else if (action.getSource() == hpm && character.getHp() > 0) {
            character.setHp(character.getHp() - 1);
            points++;
        } else if (action.getSource() == atkp && points > 0) {
            character.setAtk(character.getAtk() + 1);
            points--;
        } else if (action.getSource() == atkm && character.getAtk() > 0) {
            character.setAtk(character.getAtk() - 1);
            points++;
        } else if (action.getSource() == defp && points > 0) {
            character.setDef(character.getDef() + 1);
            points--;
        } else if (action.getSource() == defm && character.getDef() > 0) {
            character.setDef(character.getDef() - 1);
            points++;
        } else if (action.getSource() == Bconfirm) {

            // arrumar a abertura do campo de batalha
            CampoDeBatalha CampoDeBatalha = new CampoDeBatalha();
            CampoDeBatalha.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        }
        updater();
        
    }

    private void updater() {
        infohp.setText("HP: " + character.getHp());
        infoatk.setText("ATK: " + character.getAtk());
        infodef.setText("DEF: " + character.getDef());
        pointsLabel.setText("Points Left: " + points);
    }

    private ImageIcon scaleImageIcon(Hero chara) {
        ImageIcon imgbuf = new ImageIcon(chara.getPortrait().getImage());
        Image img = imgbuf.getImage();
        Image scaledImg = img.getScaledInstance(200, 200, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }
}
```

## CampoDeBatalha

```java
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;
import java.util.Random;
import javax.swing.*;

public class CampoDeBatalha extends JFrame implements ActionListener, KeyListener {

    private Hero heroi;

    JFrame campoBatalha = new JFrame();
    JButton[] botoes = new JButton[50];
    Random aleatorio = new Random();

    // Posicoes
    int posicaoHeroi = aleatorio.nextInt(9);  // Posicao do heroi aleatoria da linha inicial
    int posicaoChefao = aleatorio.nextInt(40, 49);  // Posicao do chefao aleatoria da linha final

    // Criacao de vetores para posicoes e inimigos
    ArrayList<Inimigo> vetorInimigos = new ArrayList<Inimigo>();
    ArrayList<Integer> posicoesInimigos = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasLeves = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasPesadas = new ArrayList<Integer>();
    ArrayList<Integer> posicoesWhiskey = new ArrayList<Integer>();

    // Imagens
    ImageIcon heroiIcon = new ImageIcon("imgs\\Outlaw.png");
    ImageIcon indioIcon = new ImageIcon("imgs\\Indio.png");
    ImageIcon rogueIcon = new ImageIcon("imgs\\Rogue.png");
    ImageIcon billyIcon = new ImageIcon("imgs\\Billy.png");
    ImageIcon armadilhaPesadaIcon = new ImageIcon("imgs\\Beartrap.png");
    ImageIcon armadilhaLeveIcon = new ImageIcon("imgs\\Cactus.png");
    ImageIcon whiskeyIcon = new ImageIcon("imgs\\whiskey.png");

    


    CampoDeBatalha(Hero heroi) {

        this.heroi = heroi;

        campoBatalha.setLayout(new GridLayout(5, 10)); // Grade com 50

        // Instancia 50 botoes adicionando ao frame e o ActionListener
        for (int i = 0; i < 50; i++) {
            botoes[i] = new JButton();
            botoes[i].addActionListener(this);
            campoBatalha.add(botoes[i]);

            // Deixa os botoes invisiveis (para colocar uma imagem de fundo)
            //botoes[i].setOpaque(false);
            //botoes[i].setContentAreaFilled(false);
            //botoes[i].setBorderPainted(false);
        }

        // Características do frame
        campoBatalha.setSize(800, 700);                  // Dimensoes
        campoBatalha.setTitle("Everything has a start");        // Titulo
        campoBatalha.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  // Fechar ao sair ou clicar em fechar
        campoBatalha.setResizable(true);                    // Tamanho pode ser modificado
        campoBatalha.setLocationRelativeTo(null);                   // Começa no centro
        campoBatalha.setVisible(true);                              // Visível 

        campoBatalha.addKeyListener(this);                            // Adiciona o KeyListener para deteccao de teclas
        campoBatalha.setFocusable(true);                    // Necessario para que o frame possa capturar eventos de teclado

        // Escala as imagens
        armadilhaPesadaIcon = scaleImageIcon(armadilhaPesadaIcon, 100, 100);
        armadilhaLeveIcon = scaleImageIcon(armadilhaLeveIcon, 100, 100);
        whiskeyIcon = scaleImageIcon(whiskeyIcon, 100, 100);
        indioIcon = scaleImageIcon(indioIcon, 100, 100);
        rogueIcon = scaleImageIcon(rogueIcon, 100, 100);
        billyIcon = scaleImageIcon(billyIcon, 100, 100);
        heroiIcon = scaleImageIcon(heroiIcon, 100, 100);

        // Posiciona heroi e chefao
        botoes[posicaoHeroi].setIcon(heroiIcon); // Define a imagem do heroi no botão
        botoes[posicaoChefao].setIcon(billyIcon); // Define a imagem do chefao no botão

        // Cria e distribui inimigos e armadilhas pelo campo
        distribuirArmadilhasPesadas(3);
        distribuirArmadilhasLeves(3);
        distribuirIndios(3); 
        distribuirRogues(3);
        distribuirWhiskey(4);


    }
    

    private boolean posicaoNaoEstaLivre(int posicao){
        // Garante que os inimigos nao fiquem na mesma posicao que o heroi ou entre si, nem com as armdilhas
        if (posicao == posicaoHeroi || posicao == posicaoChefao || posicoesInimigos.contains(posicao) || posicoesArmadilhasLeves.contains(posicao) || posicoesArmadilhasPesadas.contains(posicao)) {
            return true;
        }return false;
    }

    private void distribuirWhiskey(int numWhiskey) {
        for (int i = 0; i < numWhiskey; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesWhiskey.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(whiskeyIcon);  // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirArmadilhasPesadas(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasPesadas.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(armadilhaPesadaIcon);  // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirArmadilhasLeves(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasLeves.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(armadilhaLeveIcon); // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirIndios(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Indio("Indio " + (i + 1), 10, 2, 5); // Instancia os Indios
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            
            botoes[posicao].setIcon(indioIcon); // Define a imagem do inimigo no botão da posicao atual
        }
    }

    private void distribuirRogues(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Rogue("Rogue " + (i + 1), 10, 2, 5); // Instancia os rogues
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(rogueIcon); // Define a imagem do inimigo no botão da posicao atual
        }
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        for (int i = 0; i < 50; i++) {
            if (e.getSource() == botoes[i]) {
                System.out.println("Botao " + i + " pressionado");
            }
        }
    }

    @Override // Funcao para movimentar o heroi e o comeco das interacoes
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();

        botoes[posicaoHeroi].setIcon(null); // Remove a imagem do heroi do botao anterior

        // Os ifs garantem que o heroi nao vai sair para fora do campoBatalha
        switch (keyCode) {
            case KeyEvent.VK_UP:
                if (posicaoHeroi >= 10) {
                    posicaoHeroi -= 10;
                }
                break;
            case KeyEvent.VK_DOWN:
                if (posicaoHeroi < 40) {
                    posicaoHeroi += 10;
                }
                break;
            case KeyEvent.VK_LEFT:
                if (posicaoHeroi % 10 != 0) {
                    posicaoHeroi -= 1;
                }
                break;
            case KeyEvent.VK_RIGHT:
                if (posicaoHeroi % 10 != 9) {
                    posicaoHeroi += 1;
                } 
                break;
        }

        // Interagi de acordo com o que o heroi entrou em contato
        if (posicoesInimigos.contains(posicaoHeroi)) {           
            combateInimigoBasico();
        }else if (posicaoChefao == posicaoHeroi) {
            combateChefao();
        }
        else if (posicoesArmadilhasPesadas.contains(posicaoHeroi)) {
            danoArmadilhaPesada();
        } 
        else if (posicoesArmadilhasLeves.contains((posicaoHeroi))) {
            danoArmadilhaLeve();
        }
        else if (posicoesWhiskey.contains((posicaoHeroi))) {
            adicionarWhiskey();
        }
        else {
            botoes[posicaoHeroi].setIcon(heroiIcon); // Caso contrario so atualiza a posicao do heroi com a imagem
        }

    }

    @Override
    public void keyReleased(KeyEvent e) {
        // Nao utilizado
    }

    @Override
    public void keyTyped(KeyEvent e) {
        // Nao utilizado
    }

    // Implementa a logica de interacao entre heroi e inimigo (Problema para o futuro)
    private void combateInimigoBasico() {

        int indiceInimigoAtual = posicoesInimigos.indexOf(posicaoHeroi);  // Pega o indice do inimigo atual na lista
        Inimigo inimigoAtual = vetorInimigos.get(indiceInimigoAtual); // Pega o mesmo inimigo que o heroi encontrou

        new JanelaCombate(heroi, inimigoAtual); // Abre a nova janela de combate

        posicoesInimigos.remove(indiceInimigoAtual);  // Remove a posicao do inimigo derrotado
        vetorInimigos.remove(indiceInimigoAtual);     // Remove o inimigo derrotado do vetorInimigos
        botoes[posicaoHeroi].setIcon(heroiIcon);      // Atualiza o icone do heroi
    }

    // Combate com chefao (nao feito) (provavelmente vai ter que ser em uma tela nova)
    private void combateChefao() {

        JOptionPane.showMessageDialog(this, "<VOCE ENCONTROU O CHEFAO> \n<PREPARE-SE PARA BATALHA>");
        Inimigo chefao = new Chefao("Billy The Kid", 10, 20, 10); // Instancia o chefao
        new JanelaCombate(heroi, chefao); // Abre a nova janela de combate
    }

    // -0 ate -5 de hp ao contato
    private void danoArmadilhaPesada() {
        int danoPorArmadilha = aleatorio.nextInt(5);

        if (danoPorArmadilha == 0) {
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de urso, porem com muito cuidado conseguiu desarma-la\nTenha mais cuidado");    
        } else {
            heroi.setHp(heroi.getHp() - danoPorArmadilha);
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de urso, perdendo " + aleatorio.nextInt(5) + " pontos de vida\nTenha mais cuidado");
        }

        posicoesArmadilhasPesadas.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    // -1 de hp ao contato    
    private void danoArmadilhaLeve() {
        heroi.setHp(heroi.getHp() - 1);
        JOptionPane.showMessageDialog(this, "Voce bebeu tanto Whisky que acabou batendo em um cacto, perdendo 1 pontos de vida\nTa na hora de parar de beber");

        posicoesArmadilhasLeves.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    private void adicionarWhiskey() {
        JOptionPane.showMessageDialog(this, "Voce encontrou um Whiskey\nBeba com moderacao");
        heroi.setNumWhiskey(heroi.getNumWhiskey() + 1);

        posicoesWhiskey.remove(Integer.valueOf(posicaoHeroi)); // Remove o Whiskey do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    //img escalador heroi
    private ImageIcon scaleImageIconHero(Hero chara, int x, int y) {
    ImageIcon imgbuf = new ImageIcon(chara.getPortrait().getImage());
    Image img = imgbuf.getImage();
    Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
    return new ImageIcon(scaledImg);
  }
  
  //img escalador generico
    private ImageIcon scaleImageIcon(ImageIcon icon, int x, int y) {
    Image img = icon.getImage();
    Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
    return new ImageIcon(scaledImg);
  }
}
```
## JanelaCombate
```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;
import javax.swing.*;


public class JanelaCombate extends JFrame {
    private Hero heroi;          
    private Inimigo inimigoAtual; 
    private JLabel lblHeroHp, lblHeroAtk, lblHeroDef; // Labels para exibir stats do heroi
    private JLabel lblInimigoHp, lblInimigoAtk, lblInimigoDef; // Labels para exibir stats do inimigo


    public JanelaCombate(Hero heroi, Inimigo inimigoAtual) {
        this.heroi = heroi;
        this.inimigoAtual = inimigoAtual;

        // Caracteristicas da janela de combate
        setTitle("Combate com " +  inimigoAtual.getNome());   // Titulo 
        setSize(400, 300);                       // Dimensoes
        setLayout(new GridLayout(5, 2));            // Formato

        // Inicializa os labels dos stats do heroi e do inimigo
        lblHeroHp = new JLabel("HP do Heroi: " + heroi.getHp());
        lblHeroAtk = new JLabel("Atk do Heroi: " + heroi.getAtk());
        lblHeroDef = new JLabel("Def do Heroi: " + heroi.getDef());
        lblInimigoHp = new JLabel("HP do Inimigo: " + inimigoAtual.getHp());
        lblInimigoAtk = new JLabel("Atk do Inimigo: " + inimigoAtual.getAtk());
        lblInimigoDef = new JLabel("Def do Inimigo: " + inimigoAtual.getDef());

        // Botao Atacar + ActionListener
        JButton botaoAtacar = new JButton("Atacar");
        botaoAtacar.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                combate(); 
            }
        });

        // Botao Beber Whisky + ActionListener
        JButton botaoWhisky  = new JButton("Beber Whisky");
        botaoWhisky.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {

                if (heroi.getNumWhiskey() == 0 ){
                    JOptionPane.showMessageDialog(null, "Acabou o estoque camarada...");
                }else {
                    heroi.setHp(heroi.getHp() + 20); // Recupera 20 de HP, por exemplo
                    heroi.setNumWhiskey(heroi.getNumWhiskey() - 1);
                    atualizarStatusDaTela(); // Atualiza a interface com o novo valor de HP
                    JOptionPane.showMessageDialog(null, "Voce bebeu whisky e recuperou 20 de vida!");
                }    
            }
        });

        // Botao usarHabilidadeEspecial + ActionListener
        JButton botaoHabilidadeEspecial  = new JButton("Usar Habilidade Especial");
        botaoHabilidadeEspecial.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(null, "Voce usou sua Habilidade Especial!");
            }
        });

        // Botao botaFugir + ActionListener
        JButton botaFugir  = new JButton("Fugir");
        botaFugir.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(null, "Voce saiu correndo e acabou tropecando, sofrendo 3 de dano no processo... seu covarde!");
                heroi.setHp(heroi.getHp() - 3);
                dispose(); // Fecha a janela de combate
            }
        });

        // Adiciona os componentes na janela
        add(lblHeroHp);
        add(lblInimigoHp);
        add(lblHeroAtk);      
        add(lblInimigoAtk);
        add(lblHeroDef);
        add(lblInimigoDef);
        add(botaoAtacar);     
        add(botaoWhisky);
        add(botaoHabilidadeEspecial);
        add(botaFugir);

        // Mais caracteristicas da janela de combate
        setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE); // So fecha essa janela e nao toda o jogo
        setLocationRelativeTo(null); // Começa no centro
        setFocusable(true);  // Tira a 'sombra' do botao (tambem deve fazer mais alguma coisa que nao sei)
        setVisible(true);            // Visivel
    }

    // Logica de combate
    private void combate() {

        Random aleatorio = new Random();

        // Calculos para o combate
        int atkTotal = heroi.getAtk() + aleatorio.nextInt(10);
        int defTotal = inimigoAtual.getDef() + aleatorio.nextInt(10);
        int diferenca = atkTotal - defTotal;

        // Inimigo recebendo o ataque
        if (defTotal > atkTotal) {
            JOptionPane.showMessageDialog(this, "O inimigo defendou todo o seu ataque!!!");
        }
        else {
            JOptionPane.showMessageDialog(this, "Voce infligiu " + diferenca + " de dano.");
            inimigoAtual.setHp((inimigoAtual.getHp() - diferenca));  // Atualiza a vida do inimigo
        }

        // Se o inimigo nao estiver vido
        if (inimigoAtual.getHp() <= 0) {

            // Caso a luta tenha sido contra o chefao mostra mensagem de end game (precisa voltar para o menu inicial)
            if (inimigoAtual instanceof Chefao) {
                JOptionPane.showMessageDialog(this, "Parabens!!!");
                dispose(); // Fecha a janela de combate
                return;
            }

            int recompensaAleatoria = aleatorio.nextInt(3);           

            //  Concede ao heroi um atributo aleatorio
            switch (recompensaAleatoria) {
                case 0:
                    heroi.setHp(heroi.getHp() + 1);
                    JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Vida");
                    break;
                case 1:
                    heroi.setAtk(heroi.getAtk() + 1);
                    JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Ataque");
                    break;
                case 2:
                    heroi.setDef(heroi.getDef() + 1);
                    JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Defesa");
                    break;
                default:
                    System.out.println("Erro dentro do switch!");
                    throw new AssertionError();
            }

            dispose(); // Fecha a janela de combate
        } else {
            atkTotal = inimigoAtual.getAtk() + aleatorio.nextInt(10);
            defTotal = heroi.getDef() + aleatorio.nextInt(10);
            diferenca = atkTotal - defTotal;

            // Mesma logica de combate de antes mas agora com o heroi recebendo o ataque
            if (defTotal > atkTotal) {
                JOptionPane.showMessageDialog(this, "Voce defendou completamente o ataque do inimigo!!!");
            }
            else {
                JOptionPane.showMessageDialog(this, "Voce sofreu " + diferenca + " de dano.");
                heroi.setHp((heroi.getHp() - diferenca));  // Atualiza a vida do inimigo
            }
        }

        // Caso o heroi tenha morrido
        if (heroi.getHp() <= 0) {
            JOptionPane.showMessageDialog(this, "Seu HP chegou em 0, voce perdeu!\n                       :(");
            dispose(); // Fecha a janela de combate
        }

        // Refresh na tela de status
        atualizarStatusDaTela();
    }

    // Atualiza labels de HP na janela
    private void atualizarStatusDaTela() {
        lblHeroHp.setText("HP do Heroi: " + heroi.getHp());             
        lblInimigoHp.setText("Hp do Inimigo: " + inimigoAtual.getHp()); 
    }
}
```

## Field
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.*;
import java.util.Random;
import java.util.ArrayList;

class Field extends JFrame implements ActionListener, KeyListener {

    private JPanel battlefield;

    private Hero heroi;

    private ImageIcon picture;

    private JLabel infohp;
    private JLabel infoatk;
    private JLabel infodef;

    private Image battleground_img, wooden_img;

    //====================battleinfo========================

    JButton botaoDica = new JButton();
    JButton[] botoes = new JButton[50];
    Random aleatorio = new Random();

    // Posicoes
    int posicaoHeroi = aleatorio.nextInt(9);  // Posicao do heroi aleatoria da linha inicial
    int posicaoChefao = aleatorio.nextInt(40, 49);  // Posicao do chefao aleatoria da linha final

    // Criacao de vetores para posicoes e inimigos
    ArrayList<Inimigo> vetorInimigos = new ArrayList<Inimigo>();
    ArrayList<Integer> posicoesInimigos = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasLeves = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasPesadas = new ArrayList<Integer>();
    ArrayList<Integer> posicoesWhiskey = new ArrayList<Integer>();

    // Imagens
    ImageIcon heroiIcon = new ImageIcon("imgs\\Outlaw.png");
    ImageIcon indioIcon = new ImageIcon("imgs\\Indio.png");
    ImageIcon rogueIcon = new ImageIcon("imgs\\Rogue.png");
    ImageIcon billyIcon = new ImageIcon("imgs\\Billy.png");
    ImageIcon armadilhaPesadaIcon = new ImageIcon("imgs\\Beartrap.png");
    ImageIcon armadilhaLeveIcon = new ImageIcon("imgs\\Cactus.png");
    ImageIcon whiskeyIcon = new ImageIcon("imgs\\whiskey.png");

    //=============================================================================================
    public Field(Hero heroi) {
        super("Battlefield");
        this.heroi = heroi;

        // icone de janela
        ImageIcon icon = new ImageIcon("imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        // resolução e icone
        setSize(800, 480);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);

        // ============================Painel de fundo=============================

        // carregar imagem de personagem
        picture = scaleImageIconHero(heroi, 100, 100);
        JLabel Lportrait = new JLabel(picture);
        Lportrait.setBounds(650, 15, 100, 100);

        // label de info de personagem
        JLabel infohp = new JLabel("HP: " + heroi.getHp(), SwingConstants.CENTER);
        infohp.setForeground(Color.BLACK);

        JLabel infoatk = new JLabel("ATK: " + heroi.getAtk(), SwingConstants.CENTER);
        infoatk.setForeground(Color.BLACK);

        JLabel infodef = new JLabel("DEF: " + heroi.getDef(), SwingConstants.CENTER);
        infodef.setForeground(Color.BLACK);

        JPanel infodisplay = new JPanel(new GridLayout(3, 1, 0, 2));
        infodisplay.setOpaque(false);
        infodisplay.setBounds(650, 115, 100, 100);

        infodisplay.add(infohp);
        infodisplay.add(infoatk);
        infodisplay.add(infodef);

        // criando label de inventario
        JLabel Invent= new JLabel("Inventory");
        Invent.setBounds(670, 230, 70, 20);
        Invent.setForeground(Color.BLACK);

        // carregando fundos
        battleground_img = new ImageIcon("imgs/Fieldsml.png").getImage();
        wooden_img = new ImageIcon("imgs/depth.png").getImage();

        // painel de madeira
        JPanel Woodenpanel = new ImagePanel(wooden_img, 800, 480);
        Woodenpanel.setBounds(0, 0, 800, 480);
        Woodenpanel.setLayout(null);

        // painel de combate
        
        battlefield = new ImagePanel(battleground_img, 600, 400);
        battlefield.setBounds(0, 0, 600, 400);
        battlefield.setBorder(BorderFactory.createLineBorder(Color.BLACK, 2));
        battlefield.setLayout(new GridLayout(5, 10));
        battlefield.addKeyListener(this);
        battlefield.setFocusable(true);        

        // Instancia 50 botoes adicionando ao frame e o ActionListener
        for (int i = 0; i < 50; i++) {
            botoes[i] = new JButton();
            botoes[i].addActionListener(this);
            battlefield.add(botoes[i]);

            // Deixa os botoes invisiveis (para colocar uma imagem de fundo)
            botoes[i].setOpaque(false);
            botoes[i].setContentAreaFilled(false);
            botoes[i].setBorderPainted(false);
        }

        // Botao dica
        infodisplay.add(botaoDica);
        botaoDica.addActionListener(this);

        // colocando um painel no outro
        Woodenpanel.add(battlefield);
        Woodenpanel.add(Lportrait);
        Woodenpanel.add(infodisplay);
        //Woodenpanel.add(Inventory); 
        Woodenpanel.add(Invent);

        // adicionando os paineis na tela
        add(Woodenpanel);
        setVisible(true);

        // Escala as imagens
        armadilhaPesadaIcon = scaleImageIcon(armadilhaPesadaIcon, 100, 100);
        armadilhaLeveIcon = scaleImageIcon(armadilhaLeveIcon, 100, 100);
        whiskeyIcon = scaleImageIcon(whiskeyIcon, 100, 100);
        indioIcon = scaleImageIcon(indioIcon, 100, 100);
        rogueIcon = scaleImageIcon(rogueIcon, 100, 100);
        billyIcon = scaleImageIcon(billyIcon, 100, 100);
        heroiIcon = scaleImageIcon(heroiIcon, 100, 100);
        
        // Posiciona heroi e chefao
        botoes[posicaoHeroi].setIcon(heroiIcon); // Define a imagem do heroi no botao
        botoes[posicaoChefao].setIcon(billyIcon); // Define a imagem do chefao no botao

        // Cria e distribui inimigos e armadilhas pelo campo
        distribuirArmadilhasPesadas(3);
        distribuirArmadilhasLeves(3);
        distribuirIndios(3);
        distribuirRogues(3);
        distribuirWhiskey(4);
  }

    @Override
    public void actionPerformed(ActionEvent e) {
        
        // Dica
        if (e.getSource() == botaoDica) {
            if (verificarArmadilhasAoRedor()) {
                JOptionPane.showMessageDialog(this, "Tem no minimo uma armadilha ao seu redor\n                    Tome cuidado");
                battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
            } else {
                JOptionPane.showMessageDialog(this, "Nenhuma armadilha encontrada ao seu redor!");
                battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
            }
        }
        
        // Nao utilizado no momento (provavelmente deletar para o projeto final) (so usei para ajudar com as logicas do programa)
        for (int i = 0; i < 50; i++) {
            if (e.getSource() == botoes[i]) {
                System.out.println("Botao " + i + " pressionado");
                battlefield.requestFocusInWindow();
            }
        }
    }

    private boolean verificarArmadilhasAoRedor() {
        int[] direcoes = {-1, 1, -10, 10, -9, 9, -11, 11};  // Direcoes a verificar
    
        for (int i = 0; i < direcoes.length; i++) {
            
            int posicaoVerificarAtual = posicaoHeroi + direcoes[i];
    
            // Nao verificar alem do limite do campo de batalha
            if (posicaoVerificarAtual >= 0 && posicaoVerificarAtual < 50) {
                if (posicoesArmadilhasLeves.contains(posicaoVerificarAtual) || posicoesArmadilhasPesadas.contains(posicaoVerificarAtual)) {
                    return true;  
                }
            }
        }
        return false; 
    }
    
    private boolean posicaoNaoEstaLivre(int posicao){
        // Garante que os inimigos nao fiquem na mesma posicao que o heroi ou entre si, nem com as armdilhas
        if (posicao == posicaoHeroi || posicao == posicaoChefao || posicoesInimigos.contains(posicao) || posicoesArmadilhasLeves.contains(posicao) || posicoesArmadilhasPesadas.contains(posicao)) {
            return true;
        }return false;
    }

    private void distribuirWhiskey(int numWhiskey) {
        for (int i = 0; i < numWhiskey; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesWhiskey.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(whiskeyIcon);  // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirArmadilhasPesadas(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasPesadas.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(armadilhaPesadaIcon);  // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirArmadilhasLeves(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasLeves.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(armadilhaLeveIcon); // Define a imagem da armadilha no botão da posicao atual
        }
    }

    private void distribuirIndios(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Indio("Indio " + (i + 1), 10, 2, 5); // Instancia os Indios
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            
            botoes[posicao].setIcon(indioIcon); // Define a imagem do inimigo no botão da posicao atual
        }
    }

    private void distribuirRogues(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Rogue("Rogue " + (i + 1), 10, 2, 5); // Instancia os rogues
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            botoes[posicao].setIcon(rogueIcon); // Define a imagem do inimigo no botão da posicao atual
        }
    }

    @Override // Funcao para movimentar o heroi e o comeco das interacoes
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();

        botoes[posicaoHeroi].setIcon(null); // Remove a imagem do heroi do botao anterior

        // Os ifs garantem que o heroi nao vai sair para fora do campoBatalha
        switch (keyCode) {
            case KeyEvent.VK_UP:
                if (posicaoHeroi >= 10) {
                    posicaoHeroi -= 10;
                }
                break;
            case KeyEvent.VK_DOWN:
                if (posicaoHeroi < 40) {
                    posicaoHeroi += 10;
                }
                break;
            case KeyEvent.VK_LEFT:
                if (posicaoHeroi % 10 != 0) {
                    posicaoHeroi -= 1;
                }
                break;
            case KeyEvent.VK_RIGHT:
                if (posicaoHeroi % 10 != 9) {
                    posicaoHeroi += 1;
                } 
                break;
        }

        // Interagi de acordo com o que o heroi entrou em contato
        if (posicoesInimigos.contains(posicaoHeroi)) {           
            combateInimigoBasico();
        }else if (posicaoChefao == posicaoHeroi) {
            combateChefao();
        }
        else if (posicoesArmadilhasPesadas.contains(posicaoHeroi)) {
            danoArmadilhaPesada();
        } 
        else if (posicoesArmadilhasLeves.contains((posicaoHeroi))) {
            danoArmadilhaLeve();
        }
        else if (posicoesWhiskey.contains((posicaoHeroi))) {
            adicionarWhiskey();
        }
        else {
            botoes[posicaoHeroi].setIcon(heroiIcon); // Caso contrario so atualiza a posicao do heroi com a imagem
        }

        battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao

    }

    @Override
    public void keyReleased(KeyEvent e) {
        // Nao utilizado
    }

    @Override
    public void keyTyped(KeyEvent e) {
        // Nao utilizado
    }

    // Implementa a logica de interacao entre heroi e inimigo (Problema para o futuro)
    private void combateInimigoBasico() {

        int indiceInimigoAtual = posicoesInimigos.indexOf(posicaoHeroi);  // Pega o indice do inimigo atual na lista
        Inimigo inimigoAtual = vetorInimigos.get(indiceInimigoAtual); // Pega o mesmo inimigo que o heroi encontrou

        new JanelaCombate(heroi, inimigoAtual); // Abre a nova janela de combate

        posicoesInimigos.remove(indiceInimigoAtual);  // Remove a posicao do inimigo derrotado
        vetorInimigos.remove(indiceInimigoAtual);     // Remove o inimigo derrotado do vetorInimigos
        botoes[posicaoHeroi].setIcon(heroiIcon);      // Atualiza o icone do heroi
    }

    // Combate com chefao (nao feito) (provavelmente vai ter que ser em uma tela nova)
    private void combateChefao() {

        JOptionPane.showMessageDialog(this, "<VOCE ENCONTROU O CHEFAO> \n<PREPARE-SE PARA BATALHA>");
        Inimigo chefao = new Chefao("Billy The Kid", 10, 20, 10); // Instancia o chefao
        new JanelaCombate(heroi, chefao); // Abre a nova janela de combate
    }

    // -0 ate -5 de hp ao contato
    private void danoArmadilhaPesada() {
        int danoPorArmadilha = aleatorio.nextInt(5);

        if (danoPorArmadilha == 0) {
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de urso, porem com muito cuidado conseguiu desarma-la\nTenha mais cuidado");    
        } else {
            heroi.setHp(heroi.getHp() - danoPorArmadilha);
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de urso, perdendo " + aleatorio.nextInt(5) + " pontos de vida\nTenha mais cuidado");
        }

        posicoesArmadilhasPesadas.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    // -1 de hp ao contato    
    private void danoArmadilhaLeve() {
        heroi.setHp(heroi.getHp() - 1);
        JOptionPane.showMessageDialog(this, "Voce bebeu tanto Whisky que acabou batendo em um cacto, perdendo 1 pontos de vida\nTa na hora de parar de beber");

        posicoesArmadilhasLeves.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    private void adicionarWhiskey() {
        JOptionPane.showMessageDialog(this, "Voce encontrou um Whiskey\nBeba com moderacao");
        heroi.setNumWhiskey(heroi.getNumWhiskey() + 1);

        posicoesWhiskey.remove(Integer.valueOf(posicaoHeroi)); // Remove o Whiskey do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
    }

    //img escalador generico
    private ImageIcon scaleImageIcon(ImageIcon icon, int x, int y) {
        Image img = icon.getImage();
        Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

    //img escalador heroi
    private ImageIcon scaleImageIconHero(Hero chara, int x, int y) {
        ImageIcon imgbuf = new ImageIcon(chara.getPortrait().getImage());
        Image img = imgbuf.getImage();
        Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

    private void updater() {
        infohp.setText("HP: " + heroi.getHp());
        infoatk.setText("ATK: " + heroi.getAtk());
        infodef.setText("DEF: " + heroi.getDef());
    }
}
```

## Main
```java
public class main {
    public static void main(String[] args) {
        System.out.println("here");
        
        //new Mwindows();
        
        Hero heroi = new Gunslinger(100, 15, 1);
        new CampoDeBatalha(heroi);
    }
}
```