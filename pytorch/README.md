# Pytorch

## nn.ModuleList
```
"""
torch.reshape() or torch.view() # same behaviour, reshape works every time
torch.squeeze(dim=) # remove a dimension
torch.unsqueeze(dim=) # add a dimension
t.data.cpu().numpy() # no need to call t.detach() if we use .data property
t.repeat(4,1,1) # stacking the tensor t 4 times vertically
torch.cat(t1,t2)

"""
```

## nn.ModuleList
```
"""
nn.ModuleList is just like a Python list. It was designed to store any desired number of nn.Module’s. 
It may be useful, for instance, if you want to design a neural network whose number of layers is passed as input:
"""
class LinearNet(nn.Module):
  def __init__(self, input_size, num_layers, layers_size, output_size):
    super(LinearNet, self).__init__()
    self.linears = nn.ModuleList([nn.Linear(input_size, layers_size)])
    self.linears.extend([nn.Linear(layers_size, layers_size) for i in range(1, self.num_layers-1)])
    self.linears.append(nn.Linear(layers_size, output_size)
```

## nn.Sequential

```
"""
nn.Sequential allows you to build a neural net by specifying sequentially the building blocks
(nn.Module’s) of that net. Here’s an example:
"""
class Flatten(nn.Module):
  def forward(self, x):
    N, C, H, W = x.size() # read in N, C, H, W
    return x.view(N, -1)

    simple_cnn = nn.Sequential(
      nn.Conv2d(3, 32, kernel_size=7, stride=2),
      nn.ReLU(inplace=True),
      Flatten(), 
      nn.Linear(5408, 10),
    )
```
