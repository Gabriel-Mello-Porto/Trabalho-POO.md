# Trabalho-POO

## Hero
```java
abstract class Hero {
    private int hp;
    private int atk;
    private int def;

  
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
}
```
### Gunslinger
```java
import javax.swing.*;

class Gunslinger extends hero{

  ImageIcon portrait=new ImageIcon("src/imgs/Gunslinger.png");
  private boolean skill=true;

  public Gunslinger(int hp, int atk, int def){
        super(10,3,2);
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

public class BillyTheKid {

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
    //hp + -
    private JButton hpp;
    private JButton hpm;

    // atk + -
    private JButton atkp;       
    private JButton atkm;

    // def + -
    private JButton defp;
    private JButton defm;

    //imagem de personagem
    private JLabel Lportrait;

    private hero character;

    public int points = 10;
    

    public ChScreen(hero character){
        super("Character Customization");
        this.character=character;

        // icone da janela
        ImageIcon icon = new ImageIcon("src/imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        Container tela = getContentPane();
        setSize(800, 480);
        setLayout(new BorderLayout());

        Hselect backimg = new Hselect("src/imgs/src/imgs/Upgradescreen.png");

        //inicialização
        hpp = new JButton("HP+");
        hpm = new JButton("HP-");
        atkp = new JButton("ATK+");
        atkm = new JButton("ATK-");
        defp = new JButton("DEF+");
        defm = new JButton("DEF-");

        //listeners
        hpp.addActionListener(this);
        hpm.addActionListener(this);
        atkp.addActionListener(this);
        atkm.addActionListener(this);
        defp.addActionListener(this);
        defm.addActionListener(this);

        //mostrar a foto do personagem;
        Lportrait = new JLabel(character.getPortrait());

        //painel de botões
        JPanel buttonPanel = new JPanel(new GridLayout(3,2,30,100));
        buttonPanel.setOpaque(false);
        buttonPannel.setBorder(new EmptyBorder(30,30,0,0));

        //botões para o painel
        buttonPanel.add(hpp);      //1
        buttonPanel.add(hpm);     //2
        buttonPanel.add(atkp);     //1
        buttonPanel.add(atkm);     //2
        buttonPanel.add(defp);     //1
        buttonPanel.add(defm);     //2

        //adicionando os elementos na tela
        backimg.setLayout(new BorderLayout());
        backimg.add(buttonPanel, BorderLayout.WEST);  
        backimg.add(Lportrait, BorderLayout.EAST);

        //adicionando a imagem
        tela.add(backimg, BorderLayout.CENTER);

        setVisible(true);
    }

    //mar de if's para cada botão
    //
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
        }
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

    JFrame campoBatalha = new JFrame();
    JButton[] botoes = new JButton[50];
    Random aleatorio = new Random();

    // Instancia o heroi (tem que ser baseado na escolha do usuario) e tambem o chefao
    Hero heroi = new Gunslinger(100, 20, 10);
    BillyTheKid chefao = new BillyTheKid(100, 20, 10);

    // Posicoes
    int posicaoHeroi = aleatorio.nextInt(9);  // Posicao do heroi aleatoria da linha inicial
    int posicaoChefao = aleatorio.nextInt(40, 49);  // Posicao do chefao aleatoria da linha final

    // Criacao de vetores para posicoes e inimigos
    ArrayList<InimigoBasico> vetorInimigos = new ArrayList<InimigoBasico>();
    ArrayList<Integer> posicoesInimigos = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasLeves = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasPesadas = new ArrayList<Integer>();

    // Imagens
    ImageIcon heroiIcon = new ImageIcon("imgs\\Outlaw.png");
    ImageIcon indioIcon = new ImageIcon("imgs\\Indio.png");
    ImageIcon rogueIcon = new ImageIcon("imgs\\Rogue.png");
    ImageIcon billyIcon = new ImageIcon("imgs\\Billy.png");
    ImageIcon armadilhaPesadaIcon = new ImageIcon("imgs\\Beartrap.png");
    ImageIcon armadilhaLeveIcon = new ImageIcon("imgs\\Cacto.png");

    

    CampoDeBatalha() {
        campoBatalha.setLayout(new GridLayout(5, 10)); // Grade com 50

        // Instancia 50 botoes adicionando ao frame e o ActionListener
        for (int i = 0; i < 50; i++) {
            botoes[i] = new JButton();
            botoes[i].addActionListener(this);
            campoBatalha.add(botoes[i]);
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

        // Posiciona heroi e chefao
        botoes[posicaoHeroi].setIcon(heroiIcon); // Define a imagem do heroi no botão
        botoes[posicaoChefao].setIcon(billyIcon); // Define a imagem do chefao no botão

        // Cria e distribui inimigos e armadilhas pelo campo
        distribuirArmadilhasPesadas(3);
        distribuirArmadilhasLeves(3);
        distribuirIndios(3); 
        distribuirRogues(3);
        
        
    }

    private boolean posicaoNaoEstaLivre(int posicao){
        // Garante que os inimigos nao fiquem na mesma posicao que o heroi ou entre si
        if (posicao == posicaoHeroi || posicao == posicaoChefao || posicoesInimigos.contains(posicao) || posicoesArmadilhasLeves.contains(posicao) || posicoesArmadilhasPesadas.contains(posicao)) {
            return true;
        }return false;
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

            InimigoBasico inimigo = new Indio("Indio " + (i + 1), 10, 2, 5); // Instancia os Indios
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

            InimigoBasico inimigo = new Rogue("Rogue " + (i + 1), 10, 2, 5); // Instancia os rogues
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
        } 
        else if (posicaoChefao == posicaoHeroi) {
            combateChefao();
        } 
        else if (posicoesArmadilhasPesadas.contains(posicaoHeroi)) {
            danoArmadilhaPesada();
        } 
        else if (posicoesArmadilhasLeves.contains((posicaoHeroi))) {
            danoArmadilhaLeve();
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
        JOptionPane.showMessageDialog(this, "O Herói encontrou um Inimigo! Começa a batalha!");

        // Simula um combate simples
        while (heroi.getHp() > 0 && vetorInimigos.get(posicoesInimigos.indexOf(posicaoHeroi)).getHp() > 0) {
            InimigoBasico inimigo = vetorInimigos.get(posicoesInimigos.indexOf(posicaoHeroi));
            inimigo.setHp(inimigo.getHp() - heroi.getAtk());
            if (inimigo.getHp() > 0) {
                heroi.setHp(heroi.getHp() - inimigo.getAtk());
            }
        }

        if (heroi.getHp() > 0) {
            JOptionPane.showMessageDialog(this, "O Herói derrotou o Inimigo!");
            botoes[posicaoHeroi].setIcon(heroiIcon); // O heroi ocupa o lugar do inimigo derrotado
        } else {
            JOptionPane.showMessageDialog(this, "O Herói foi derrotado...");
        }
    }

    // Combate com chefao (nao feito) (provavelmente vai ter que ser em uma tela nova)
    private void combateChefao() {
        JOptionPane.showMessageDialog(this, "O Herói encontrou um Inimigo! Começa a batalha!");

        // Simula um combate simples
        while (heroi.getHp() > 0 && vetorInimigos.get(posicoesInimigos.indexOf(posicaoHeroi)).getHp() > 0) {
            InimigoBasico inimigo = vetorInimigos.get(posicoesInimigos.indexOf(posicaoHeroi));
            inimigo.setHp(inimigo.getHp() - heroi.getAtk());
            if (inimigo.getHp() > 0) {
                heroi.setHp(heroi.getHp() - inimigo.getAtk());
            }
        }

        if (heroi.getHp() > 0) {
            JOptionPane.showMessageDialog(this, "O Herói derrotou o Inimigo!");
            botoes[posicaoHeroi].setIcon(heroiIcon); // O heroi ocupa o lugar do inimigo derrotado
        } else {
            JOptionPane.showMessageDialog(this, "O Herói foi derrotado...");
        }
    }

    // -1 de hp ao contato
    private void danoArmadilhaPesada() {
        System.out.println("hp antes da armadilha pesada " + heroi.getHp());
        heroi.setHp(heroi.getHp() - aleatorio.nextInt(5));
        System.out.printf("hp apos da armadilha pesada " + heroi.getHp() + "\n\n");
    }

    // -0 ate -5 de hp ao contato
    private void danoArmadilhaLeve() {
        System.out.println("hp antes da armadilha leve " + heroi.getHp());
        heroi.setHp(heroi.getHp() - 1);
        System.out.printf("hp apos da armadilha leve " + heroi.getHp() + "\n\n");
    }

    public static void main(String[] args) {
        new CampoDeBatalha();
    }
}
```

## Main
```java
import javax.swing.*;

public class Main {
  public static void main(String[] args) {
    Mwindows Mwindow = new Mwindows();

    Mwindow.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
  }
}
```