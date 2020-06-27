# chess

vazio = ' '
game = True
pecas = []

# Cores
c = '\033[1;31m'  # Vermelho
d = '\033[33m'  # Amarelo
q = '\033[1;32m'  # Verde
x = '\033[4m'  # Sublinhado
_ = '\033[m'

# Peças Brancas
brancas = {'torre': ('Bt1', 'Bt2'), 'cavalo': ('Bc1', 'Bc2'), 'bispo': ('Bb1', 'Bb2'), 'R': ('Bra', 'Bre'),
           'piao': ('Bp1', 'Bp2', 'Bp3', 'Bp4', 'Bp5', 'Bp6', 'Bp7', 'Bp8')}

# Peças Pretas
pretas = {'torre': ('Pt1', 'Pt2'), 'cavalo': ('Pc1', 'Pc2'), 'bispo': ('Pb1', 'Pb2'), 'R': ('Pra', 'Pre'),
          'piao': ('Pp1', 'Pp2', 'Pp3', 'Pp4', 'Pp5', 'Pp6', 'Pp7', 'Pp8')}

pecas.append(brancas)
pecas.append(pretas)

tabuleiro = [pecas[0]['torre'][0], pecas[0]['cavalo'][0], pecas[0]['bispo'][0], pecas[0]['R'][0], pecas[0]['R'][1],
             pecas[0]['bispo'][1], pecas[0]['cavalo'][1], pecas[0]['torre'][1],
             pecas[0]['piao'][0], pecas[0]['piao'][1], pecas[0]['piao'][2], pecas[0]['piao'][3], pecas[0]['piao'][4],
             pecas[0]['piao'][5], pecas[0]['piao'][6], pecas[0]['piao'][7],
             vazio, vazio, vazio, vazio, vazio, vazio, vazio, vazio,
             vazio, vazio, vazio, vazio, vazio, vazio, vazio, vazio,
             vazio, vazio, vazio, vazio, vazio, vazio, vazio, vazio,
             vazio, vazio, vazio, vazio, vazio, vazio, vazio, vazio,
             pecas[1]['piao'][0], pecas[1]['piao'][1], pecas[1]['piao'][2], pecas[1]['piao'][3], pecas[1]['piao'][4],
             pecas[1]['piao'][5], pecas[1]['piao'][6], pecas[1]['piao'][7],
             pecas[1]['torre'][0], pecas[1]['cavalo'][0], pecas[1]['bispo'][0], pecas[1]['R'][0], pecas[1]['R'][1],
             pecas[1]['bispo'][1], pecas[1]['cavalo'][1], pecas[1]['torre'][1]]

for tab in range(0, len(tabuleiro), 8):
    print(
        f'[{tab:^3}][{tab + 1:^3}][{tab + 2:^3}][{tab + 3:^3}][{tab + 4:^3}][{tab + 5:^3}][{tab + 6:^3}][{tab + 7:^3}]'
        f'     |     [{tabuleiro[tab]:^3}][{tabuleiro[tab + 1]:^3}][{tabuleiro[tab + 2]:^3}][{tabuleiro[tab + 3]:^3}]'
        f'[{tabuleiro[tab + 4]:^3}][{tabuleiro[tab + 5]:^3}][{tabuleiro[tab + 6]:^3}][{tabuleiro[tab + 7]:^3}]')

print()


def piaoB(peca):
  global prox
  pp = tabuleiro.index(peca)
  prox = True
  
  while True:
    if vazio in tabuleiro[pp + 8]:
      if tabuleiro.index(peca) in range(8, 16):
        if tabuleiro[pp + 7][0] == 'P' or tabuleiro[pp + 9][0] == 'P':
          while True:
            atk = int(input('Qual posição deseja atacar? [999 para não atacar] '))
            if atk == pp + 7 or atk == pp + 9:
              tabuleiro.insert(atk, peca)
              tabuleiro.pop(atk + 1)
              tabuleiro.insert(pp, vazio)
              tabuleiro.pop(pp + 1)
              prox = False
              break
            elif atk == 999:
              break
            else:
              print(f'{c}Posição inválida{_}')
        else:
          while True:
            p = int(input('Em que posição deseja move-lá? '))
            if p == pp + 8 or p == pp + 16:
              if vazio in tabuleiro[p]:
                tabuleiro.insert(p, peca)
                tabuleiro.pop(p + 1)
                tabuleiro.insert(pp, vazio)
                tabuleiro.pop(pp + 1)
                prox = False
                break
              else:
                print(f'{c}Peça incapaz de ser movida{_}')
                break
            else:
              print(f'{c}Posição inválida{_}')
              break
    else:
      if tabuleiro[pp + 7][0] == 'P' or tabuleiro[pp + 9][0] == 'P':
        while True:
          atk = int(input('Qual posição deseja atacar? [999 para não atacar] '))
            if atk == pp + 7 or atk == pp + 9:
              tabuleiro.insert(atk, peca)
              tabuleiro.pop(atk + 1)
              tabuleiro.insert(pp, vazio)
              tabuleiro.pop(pp + 1)
              prox = False
              break
            elif atk == 999:
              tabuleiro.insert(pp + 8, peca)
              tabuleiro.pop(pp + 9)
              tabuleiro.insert(pp, vazio)
              tabuleiro.pop(pp + 1)
              prox = False
              break
            else:
              print(f'{c}Posição inválida{_}')
      else:
        tabuleiro.insert(pp + 8, peca)
        tabuleiro.pop(pp + 9)
        tabuleiro.insert(pp, vazio)
        tabuleiro.pop(pp + 1)
        prox = False
        break
      break
    elif tabuleiro[pp + 7][0] == 'P' or tabuleiro[pp + 9][0] == 'P':
      atk = int(input('Qual posição você deseja atacar? '))
      if atk == pp + 7 or atk == pp + 9:
        tabuleiro.insert(atk, peca)
        tabuleiro.pop(atk + 1)
        tabuleiro.insert(pp, vazio)
        tabuleiro.pop(pp + 1)
        prox = False
        break
      else:
        print(f'{c}Ataque inválido{_}')
    else:
      print(f'{c}Peça incapaz de ser movida{_}')
      break

def piaoP(peca):
  global prox
  pp = tabuleiro.index(peca)
  prox = True
  
  while True:
    if vazio in tabuleiro[pp - 8]:
      if tabuleiro.index(peca) in range(48, 56):
        if tabuleiro[pp - 7][0] == 'B' or tabuleiro[pp - 9][0] == 'B':
          while True:
            atk = int(input('Qual posição deseja atacar? [999 para não atacar] '))
            if atk == pp - 7 or atk == pp - 9:
              tabuleiro.insert(atk, peca)
              tabuleiro.pop(atk + 1)
              tabuleiro.insert(pp, vazio)
              tabuleiro.pop(pp + 1)
              prox = False
              break
            elif atk == 999:
              break
        else:
          print(f'{c}Posição inválida{_}')
      else:
        while True:
          p = int(input('Em que posição deseja move-lá? '))
          if p == pp - 8 or p == pp - 16:
            if vazio in tabuleiro[p]:
              tabuleiro.insert(p, peca)
              tabuleiro.pop(p + 1)
              tabuleiro.insert(pp, vazio)
              tabuleiro.pop(pp + 1)
              prox = False
              break
            else:
              print(f'{c}Peça incapz de ser movida{_}')
          else:
            print(f'{c}Posição inválida{_}')
            break
    else:
      if tabuleiro[pp - 7][0] == 'B' or tabuleiro[pp - 9][0] == 'B':
        while True:
          atk = int(input('Qual posição deseja atacar? [999 para não atacar] '))
          if atk == pp - 7 or atk == pp - 9:
            tabuleiro.insert(atk, peca)
            tabuleiro.pop(atk + 1)
            tabuleiro.insert(pp, vazio)
            tabuleiro.pop(pp + 1)
            prox = False
            break
          elif atk == 999:
            tabuleiro.insert(pp - 8, peca)
            tabuleiro.pop(pp - 7)
            tabuleiro.insert(pp, vazio)
            tabuleiro.pop(pp + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
      else:
        tabuleiro.insert(pp - 8, peca)
        tabuleiro.pop(pp - 7)
        tabuleiro.insert(pp, vazio)
        tabuleiro.pop(pp + 1)
        prox = False
        break
      break
    elif tabuleiro[pp - 7][0] == 'B' or tabuleiro[pp - 9][0] == 'B':
      atk = int(input('Qual posição você deseja atacar? '))
      if atk == pp - 7 or atk == pp - 9:
        tabuleiro.insert(atk, peca)
        tabuleiro.pop(atk + 1)
        tabuleiro.insert(pp, vazio)
        tabuleiro.pop(pp + 1)
        prox = False
        break
      else:
        print(f'{c}Ataque inválido{_}')
    else:
      print(f'{c}Peça incapaz de ser movida{_}')
      break

def cavaloB(peca):
  global prox
  pc = tabuleiro.index(peca)
  prox = True
  while True:
    p = int(input('Qual posição deseja mover/atacar? '))
    if p == pc + 10 or p == pc + 17 or p == pc + 15 or p == pc + 6 or p == pc - 10 or p == pc - 17 or p == pc - 15 or p == pc - 6:
      if tabuleiro[p] == vazio or tabuleiro[p][0] == 'P':
        tabuleiro.insert(p, peca)
        tabuleiro.pop(p + 1)
        tabuleiro.insert(pc, vazio)
        tabuleiro.pop(pc + 1)
        prox = False
        break
      elif tabuleiro[p][0] == 'B':
        print(f'{c}Posição inválida{_}')
      else:
        print(f'{c}Posição inválida{_}')
        break

def cavaloP(peca):
  global prox
  pc = tabuleiro.index(peca)
  prox = True
  while True:
    p = int(input('Qual posição deseja mover/atacar? '))
      if p == pc + 10 or p == pc + 17 or p == pc + 15 or p == pc + 6 or p == pc - 10 or p == pc - 17 or p == pc - 15 or p == pc - 6:
        if tabuleiro[p] == vazio or tabuleiro[p][0] == 'B':
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pc, vazio)
          tabuleiro.pop(pc + 1)
          prox = False
          break
        elif tabuleiro[p][0] == 'P':
          print(f'{c}Posição inválida{_}')
        else:
          print(f'{c}Posição inválida{_}')
          break

def bispoB(peca):
  global prox
  pb = tabuleiro.index(peca)
  prox = True
  
  while True:
    countp = 0
    p = int(input('Qual posição deseja mover/atacar? '))
    if tabuleiro[p][0] == 'P' or tabuleiro[p] == vazio:
      if p in range(pb, p + 1, 9):
        f1 = tabuleiro[pb + 9:p:9]
        for s in f1:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb, p - 1, -9):
        f2 = tabuleiro[pb - 9:p:-9]
        for s in f2:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb, p + 1, 7):
        f3 = tabuleiro[pb + 7:p:7]
        for s in f3:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb - 7, p - 1, -7):
        f4 = tabuleiro[pb - 7:p:-7]
        for s in f4:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
    else:
      print(f'{c}Posição inválida{_}')
      break

def bispoP(peca):
  global prox
  pb = tabuleiro.index(peca)
  prox = True
  
  while True:
    countp = 0
    p = int(input('Em que posição deseja mover/atacar? '))
    if tabuleiro[p][0] == 'B' or tabuleiro[p] == vazio:
      if p in range(pb, p - 1, -9):
        f1 = tabuleiro[pb - 9:p:-9]
        for s in f1:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb, p + 1, 9):
        f2 = tabuleiro[pb + 9:p:9]
        for s in f2:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb, p - 1, -7):
        f3 = tabuleiro[pb - 7:p:-7]
        for s in f3:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pb, p + 1, 7):
        f4 = tabuleiro[pb + 7:p:7]
        for s in f4:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pb, vazio)
          tabuleiro.pop(pb + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
    else:
      print(f'{c}Posição inválida{_}')
      break

def torreB(peca):
  global prox
  pt = tabuleiro.index(peca)
  prox = True
  
  while True:
    countp = 0
    p = int(input('Em que posição deseja mover/atacar? '))
    if tabuleiro[p][0] == 'P' or tabuleiro[p] == vazio:
      if p in range(pt, p + 1, 8):
        f1 = tabuleiro[pt + 8:p:8]
        for s in f1:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p + 1, 1):
        f2 = tabuleiro[pt + 1:p:1]
        for s in f2:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p - 1, -8):
        f3 = tabuleiro[pt - 8:p:-8]
        for s in f3:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p - 1, -1):
        f4 = tabuleiro[pt - 1:p:-1]
        for s in f4:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
    else:
      print(f'{c}Posição inválida{_}')
      break

def torreP(peca):
  global prox
  pt = tabuleiro.index(peca)
  prox = True

  while True:
    countp = 0
    p = int(input('Em que posição deseja mover/atacar? '))
    if tabuleiro[p][0] == 'B' or tabuleiro[p] == vazio:
      if p in range(pt, p - 1, -8):
        f1 = tabuleiro[pt - 8:p:-8]
        for s in f1:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p + 1, 8):
        f2 = tabuleiro[pt + 8:p:8]
        for s in f2:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p - 1, -1):
        f3 = tabuleiro[pt - 1:p:-1]
        for s in f3:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pt, p + 1, 1):
        f4 = tabuleiro[pt + 1:p:1]
        for s in f4:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pt, vazio)
          tabuleiro.pop(pt + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
    else:
      print(f'{c}Posição inválida{_}')
      break

def damaB(peca):
  global prox
  pd = tabuleiro.index(peca)
  prox = True

  while True:
    countp = 0
    p = int(input('Em que posição deseja mover/atacar? '))
    if tabuleiro[p][0] == 'P' or tabuleiro[p] == vazio:
      if p in range(pd, p + 1, 8):
        f1 = tabuleiro[pd + 8:p:8]
        for s in f1:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p - 1, -8):
        f2 = tabuleiro[pd - 8:p:-8]
        for s in f2:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p + 1, 9):
        f3 = tabuleiro[pd + 9:p:9]
        for s in f3:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p + 1, 7):
        f4 = tabuleiro[pd + 7:p:7]
        for s in f4:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p - 1, -9):
        f5 = tabuleiro[pd - 9:p:-9]
        for s in f5:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p - 1, -7):
        f6 = tabuleiro[pd - 7:p:-7]
        for s in f6:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p + 1, 1):
        f7 = tabuleiro[pd + 1:p:1]
        for s in f7:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      elif p in range(pd, p - 1, -1):
        f8 = tabuleiro[pd - 1:p:-1]
        for s in f8:
          if s != vazio:
            countp += 1
        if countp == 0:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pd, vazio)
          tabuleiro.pop(pd + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
    else: 
      print(f'{c}Posição inválida{_}')
      break

def damaP(peca):
  global prox
  pd = tabuleiro.index(peca)
  prox = True

  while True:
    countp = 0
    p = int(input('Em que posição deseja mover/atacar? '))
      if tabuleiro[p][0] == 'B' or tabuleiro[p] == vazio:
        if p in range(pd, p - 1, -8):
          f1 = tabuleiro[pd - 8:p:-8]
          for s in f1:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p + 1, 8):
          f2 = tabuleiro[pd + 8:p:8]
          for s in f2:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p - 1, -7):
          f3 = tabuleiro[pd - 7:p:-7]
          for s in f3:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p - 1, -9):
          f4 = tabuleiro[pd - 9:p:-9]
          for s in f4:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p + 1, 7):
          f5 = tabuleiro[pd + 7:p:7]
          for s in f5:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p + 1, 9):
          f6 = tabuleiro[pd + 9:p:9]
          for s in f6:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p - 1, -1):
          f7 = tabuleiro[pd - 1:p:-1]
          for s in f7:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
        elif p in range(pd, p + 1, 1):
          f8 = tabuleiro[pd + 1:p:1]
          for s in f8:
            if s != vazio:
              countp += 1
          if countp == 0:
            tabuleiro.insert(p, peca)
            tabuleiro.pop(p + 1)
            tabuleiro.insert(pd, vazio)
            tabuleiro.pop(pd + 1)
            prox = False
            break
          else:
            print(f'{c}Posição inválida{_}')
      else:
        print(f'{c}Posição inválida{_}')
        break

def reiB(peca):
  global prox
  pr = tabuleiro.index(peca)
  prox = True

  while True:
    p = int(input('Em quem posição deseja mover/atacar? '))
      if tabuleiro[p][0] == 'P' or tabuleiro[p] == vazio:
        if p == pr + 1 or p == pr - 1 or p == pr + 8 or p == pr - 8 or p == pr + 9 or p == pr - 9 or p == pr + 7 \
            or p == pr - 7:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pr, vazio)
          tabuleiro.pop(pr + 1)
          prox = False
          break
        else:
          print(f'{c}Posição Inválida{_}')
      else:
        print(f'{c}Posiçãp inválida{_}')
        break

def reiP(peca):
  global prox
  pr = tabuleiro.index(peca)
  prox = True

  while True:
    p = int(input('Em que posição deseja mover/atacar? '))
      if tabuleiro[p][0] == 'B' or tabuleiro[p] == vazio:
        if p == pr + 1 or p == pr - 1 or p == pr + 8 or p == pr - 8 or p == pr + 9 or p == pr - 9 or p == pr + 7 \
            or p == pr - 7:
          tabuleiro.insert(p, peca)
          tabuleiro.pop(p + 1)
          tabuleiro.insert(pr, vazio)
          tabuleiro.pop(pr + 1)
          prox = False
          break
        else:
          print(f'{c}Posição inválida{_}')
      else:
        print(f'{c}Posição inválida{_}')

# Programa do Jogo
while game:
  prox = True
  print(f'{d}={_}' * 91)
  if 'Bre' in tabuleiro and 'Pre' in tabuleiro:
    while prox:
      jogada1 = str(input('Qual peça deseja jogar?[B] ')).title()
      if jogada1 in tabuleiro:
        if jogada1 in brancas['piao']:
          if jogada1 == 'Bp1':
            piaoB(jogada1)
          if jogada1 == 'Bp2':
            piaoB(jogada1)
          if jogada1 == 'Bp3':
            piaoB(jogada1)
          if jogada1 == 'Bp4':
            piaoB(jogada1)
          if jogada1 == 'Bp5':
            piaoB(jogada1)
          if jogada1 == 'Bp6':
            piaoB(jogada1)
          if jogada1 == 'Bp7':
            piaoB(jogada1)
          if jogada1 == 'Bp8':
            piaoB(jogada1)
        if jogada1 in brancas['cavalo']:
          if jogada1 == 'Bc1':
            cavaloB(jogada1)
          if jogada1 == 'Bc2':
            cavaloB(jogada1)
        if jogada1 in brancas['bispo']:
          if jogada1 == 'Bb1':
            bispoB(jogada1)
          if jogada1 == 'Bb2':
            bispoB(jogada1)
        if jogada1 in brancas['torre']:
          if jogada1 == 'Bt1':
            torreB(jogada1)
          if jogada1 == 'Bt2':
            torreB(jogada1)
        if jogada1 in brancas['R']:
          if jogada1 == 'Bra':
            damaB(jogada1)
          if jogada1 == 'Bre':
            reiB(jogada1)
      else:
        print(f'{c}Peça inválida{_}')
          for tab in range(0, len(tabuleiro), 8):
            print(
                f'[{tab:^3}][{tab + 1:^3}][{tab + 2:^3}][{tab + 3:^3}][{tab + 4:^3}][{tab + 5:^3}][{tab + 6:^3}][{tab + 7:^3}]'
                f'     |     [{tabuleiro[tab]:^3}][{tabuleiro[tab + 1]:^3}][{tabuleiro[tab + 2]:^3}][{tabuleiro[tab + 3]:^3}]'
                f'[{tabuleiro[tab + 4]:^3}][{tabuleiro[tab + 5]:^3}][{tabuleiro[tab + 6]:^3}][{tabuleiro[tab + 7]:^3}]')
  else:
      game = False
  prox = True
  print(f'{d}={_}' * 91)
  if 'Bre' in tabuleiro and 'Pre' in tabuleiro:
    while prox:
      jogada2 = str(input('Qual peça deseja jogar?[P] ')).title()
      if jogada2 in tabuleiro:
        if jogada2 in pretas['piao']:
          if jogada2 == 'Pp1':
            piaoP(jogada2)
          if jogada2 == 'Pp2':
            piaoP(jogada2)
          if jogada2 == 'Pp3':
            piaoP(jogada2)
          if jogada2 == 'Pp4':
            piaoP(jogada2)
          if jogada2 == 'Pp5':
            piaoP(jogada2)
          if jogada2 == 'Pp6':
            piaoP(jogada2)
          if jogada2 == 'Pp7':
            piaoP(jogada2)
          if jogada2 == 'Pp8':
            piaoP(jogada2)
        if jogada2 in pretas['cavalo']:
          if jogada2 == 'Pc1':
            cavaloP(jogada2)
          if jogada2 == 'Pc2':
            cavaloP(jogada2)
        if jogada2 in pretas['bispo']:
          if jogada2 == 'Pb1':
            bispoP(jogada2)
          if jogada2 == 'Pb2':
            bispoP(jogada2)
        if jogada2 in pretas['torre']:
          if jogada2 == 'Pt1':
            torreP(jogada2)
          if jogada2 == 'Pt2':
            torreP(jogada2)
        if jogada2 in pretas['R']:
          if jogada2 == 'Pra':
            damaP(jogada2)
          if jogada2 == 'Pre':
            damaP(jogada2)
      else:
        print(f'{c}Peça inválida{_}')
          for tab in range(0, len(tabuleiro), 8):
            print(
                f'[{tab:^3}][{tab + 1:^3}][{tab + 2:^3}][{tab + 3:^3}][{tab + 4:^3}][{tab + 5:^3}][{tab + 6:^3}][{tab + 7:^3}]'
                f'     |     [{tabuleiro[tab]:^3}][{tabuleiro[tab + 1]:^3}][{tabuleiro[tab + 2]:^3}][{tabuleiro[tab + 3]:^3}]'
                f'[{tabuleiro[tab + 4]:^3}][{tabuleiro[tab + 5]:^3}][{tabuleiro[tab + 6]:^3}][{tabuleiro[tab + 7]:^3}]')
  else:
    game = False
print('ACABOU O JOGO')
if 'Bre' in tabuleiro:
  print(f'{q}VITÓRIA{_} DAS {x}BRANCAS{_}')
else:
  print(f'{q}VITÓRIA{_} DAS {x}PRETAS{_}')
